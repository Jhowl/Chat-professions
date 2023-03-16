<script>
	import { onMount } from 'svelte';
	import Conversation from './components/Conversation.svelte'
	import ChatbotOptions from './components/ChatbotOptions.svelte'
	import UserInput from './components/UserInput.svelte'

	let currentChatbot = 'bot1';

	let conversation = [
	  { isUser: false, text: 'Hello, I am a chatbot.' },
	  { isUser: true, text: 'How can I help you?' }];

	async function sendMessage(e) {
		console.log('Sending message', e.detail);
    console.log(currentChatbot)
	//   const response = await fetch(`/api/chatbot/${currentChatbot}`, {
	// 	method: 'POST',
	// 	body: JSON.stringify({ text }),
	// 	headers: { 'Content-Type': 'application/json' }
	//   });
	//   const data = await response.json();
  conversation = [...conversation, { isUser: true, text: e.detail }];
	  // conversation.push({ isUser: true, text: e.detail });
	//   conversation.push({ isUser: false, text: data.response });
	}

  function changeChatbot(e) {
    currentChatbot = e.detail;
  }

	onMount(async () => {
	//   const response = await fetch(`/api/chatbot/${currentChatbot}`);
	//   const data = await response.json();
	//   conversation.push({ isUser: false, text: data.greeting });
	});
</script>

<div class="chat-container">
	<ChatbotOptions on:changeChatbot={changeChatbot} />
	<div class="conversation-container">
	  <Conversation conversation={conversation} />
	  <UserInput on:sendMessage={sendMessage} />
	</div>
</div>

<style>
	.chat-container {
	  display: flex;
	  height: 100vh;
	}

	.conversation-container {
	  flex: 1;
	  display: flex;
	  flex-direction: column;
	}

	@media screen and (min-width: 768px) {
	  .chat-container {
		flex-direction: row;
	  }
	}
</style>
