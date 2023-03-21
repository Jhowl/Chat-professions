<script>
  import { Configuration, OpenAIApi } from "openai"

	import Conversation from './components/Conversation.svelte'
	import ChatbotOptions from './components/ChatbotOptions.svelte'
	import UserInput from './components/UserInput.svelte'

  const configuration = new Configuration({
    apiKey: "",
  });

  const openai = new OpenAIApi(configuration);

	let conversation = {
    messages: [
	    { isUser: false, text: 'Hello, Eu sou especialista.' },
    ],
    loading: false
  };

  let bot = {}

  async function changeChatbot(e) {
    bot = e.detail
    console.log(bot)
    conversation = {
      messages: [
        { isUser: false, text: `Faça sua solitacao para o: ${bot.value}` },
      ],
      loading: false
    };
  }

	async function sendMessage(e) {
    const system = bot.prompt + "And every response you be in portuguese."

    conversation.messages = [...conversation.messages, { isUser: true, text: e.detail }]
    conversation.loading = true

    const messages = conversation.messages.map((message) => {
      return {
        role: message.isUser ? "user" : "assistant",
        content: message.text,
      }
    })

    const response = await openai.createChatCompletion({
      model: "gpt-3.5-turbo",
      messages: [
        {role: "system", content: system},
        ...messages,
      ],
    })

    if (response.data.choices.length === 0) {
      conversation.messages = [...conversation.messages, { isUser: false, text: 'I am not sure I understand.' }];
      return;
    }

    conversation.loading = false
    conversation.messages = [...conversation.messages, { isUser: false, text: response.data.choices[0].message.content }];
  }

</script>

<div class="chat-container">
	<ChatbotOptions on:changeChatbot={changeChatbot} />

	<div class="conversation-container" class:has-bot={Object.keys(bot).length === 0}>
	  <Conversation conversation={conversation} />
	  <UserInput on:sendMessage={sendMessage} />
	</div>
</div>

<style>
	.chat-container {
	  display: flex;
	  height: 100%;
    width: 100%;
    justify-content: space-evenly;
	}

	.conversation-container {
    display: block;
    width: 45%;
	  display: flex;
	  flex-direction: column;
    margin-top: 10px;
    margin-bottom: 40px;
    height: 100%;
	}

  .conversation-container.has-bot {
    display: none;
  }

	@media screen and (min-width: 768px) {
	  .chat-container {
		  flex-direction: row;
	  }
	}
</style>
