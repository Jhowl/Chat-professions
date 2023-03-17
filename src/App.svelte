<script>
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
	}

</script>

<div class="chat-container">
	<ChatbotOptions />

	<div class="conversation-container">
	  <Conversation conversation={conversation} />
	  <UserInput on:sendMessage={sendMessage} />
	</div>
</div>

<style>
	.chat-container {
	  display: flex;
	  height: 100%;
    width: 100%;
    /* border: 40px solid black; */
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

	@media screen and (min-width: 768px) {
	  .chat-container {
		  flex-direction: row;
	  }
	}
</style>
