# LiteLLM Integration

Follow these instructions to integrate AccuKnox LLM Defense with LiteLLM. This setup will enable scanning of prompts and responses for potential threats and logging interactions to enhance security and visibility for your LLM applications.

1. Install `litellm` python package, `litellm` proxy cli package and `accuknox-llm-defense` package using:

    ```bash
    pip install litellm 'litellm[proxy]' accuknox-llm-defense
    ```

2. Create the following file (`custom_callbacks.py`) in your project directory:

    ```python
    from litellm.integrations.custom_logger import CustomLogger
    import litellm
    import logging
    import json
    import yaml
    from accuknox_llm_defense import LLMDefenseClient

    # read yaml file
    with open("config.yaml", "r") as file:
        config = yaml.safe_load(file)

    # get values to set accuknox client
    token_dev_litellm = config.get('accuknox_settings').get('env_token')
    user_info = config.get('accuknox_settings').get('user_info')
    client_info = config.get('accuknox_settings').get('client_info')

    # Initialize accuknox client
    accuknox_client = LLMDefenseClient(
        llm_defense_api_key=token_dev_litellm,
        user_info=user_info,
        client_info=client_info
    )

    # This function includes the custom callbacks for LiteLLM Proxy
    # Once defined, these can be passed in proxy_config.yaml
    class MyCustomHandler(CustomLogger):
        def log_pre_api_call(self, model, messages, kwargs):
            # extract prompt and send to accuknox for logging and evaluating
            prompt = messages[0].get("content")
            sanitized_prompt = accuknox_client.scan_prompt(content=prompt)
            self.session_id = sanitized_prompt.get('session_id')

        def log_post_api_call(self, kwargs, response_obj, start_time, end_time):
            # extract response and send to accuknox for logging and evaluating
            prompt = kwargs.get('input')[0].get('content')
            original_response = json.loads(kwargs.get('original_response'))
            try:
                response = original_response['choices'][0]['message']['content']
            except (KeyError, IndexError, TypeError):
                # Fallback to alternate structure (anthropic)
                response = original_response['content'][0]['text']

            sanitized_output = accuknox_client.scan_response(
                prompt=prompt,
                content=response,
                session_id=self.session_id
            )

        def log_success_event(self, kwargs, response_obj, start_time, end_time):
            print("both prompt and response passed validation")

        def log_failure_event(self, kwargs, response_obj, start_time, end_time):
            print("failed validation on prompt/response")

        async def async_log_prompts(self, kwargs, response_obj, start_time, end_time):
            try:
                # init logging config
                logging.basicConfig(
                    filename='cost.log',
                    level=logging.INFO,
                    format='%(asctime)s - %(message)s',
                    datefmt='%Y-%m-%d %H:%M:%S'
                )

                # logging prompt to accuknox
                # Note: prompt variable usage here seems to assume it's available in scope or needs adjustment based on original code context
                # keeping as provided in snippet
                # sanitized_prompt = accuknox_client.scan_prompt(content=prompt)

                response_cost: Optional[float] = kwargs.get("response_cost", None)
                print("regular response_cost", response_cost)
                logging.info(f"Model {response_obj.model} Cost: ${response_cost:.8f}")
            except:
                pass

    accuknox_handler = MyCustomHandler()
    ```

3. Also create the following config file for the litellm proxy server (`config.yaml`):

    ```yaml
    model_list:
      - model_name: gpt-3.5-turbo
        litellm_params:
          model: gpt-3.5-turbo
          api_key: <your open-ai key>

    litellm_settings:
      callbacks: ["custom_callbacks.accuknox_handler"]

    accuknox_settings:
      env_token: <accuknox token you get when onboarding application>
      user_info: <user name/email>
      client_info: <optional client info>
    ```

4. Run the proxy server using:

    ```bash
    litellm --config <path to yaml file>
    ```

    CURL for using openai proxy, other proxies can be found [here](https://docs.litellm.ai/docs/supported_endpoints).

    ```bash
    curl --location 'http://0.0.0.0:4000/chat/completions' \
    --header 'Content-Type: application/json' \
    --data '{
      "model": "gpt-3.5-turbo",
      "messages": [
        {
          "role": "user",
          "content": "today is 4th november"
        }
      ],
      "user": "arush-app",
      "temperature": 0.2
    }'
    ```

### Findings

![alt text](image-56.png)

### Chat

![alt text](image-57.png)

This integration secures your LLM interactions by routing them through the LiteLLM proxy with AccuKnox's defense mechanisms. You can now monitor usage, detect vulnerabilities, and ensure compliance in real-time.