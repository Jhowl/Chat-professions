<script>
	import { createEventDispatcher } from 'svelte';
  // import Conversation from './components/Conversation.svelte'

  // let currentChatbot = 'bot1';
  let text = '';

  const dispatch = createEventDispatcher();

  function sendMessage() {
    dispatch('sendMessage', text);
    text = '';
  }


</script>

<div class="user-input">
  <form on:submit|preventDefault={sendMessage}>
    <textarea
      bind:value={text}
      placeholder="Type your message here"
      rows="2"
    ></textarea>
    <button type="submit">Send</button>
  </form>
</div>

<style>
  .user-input {
    display: block;
    align-items: center;
    padding: 1rem;
    background-color: #eee;
    width: 100%;
  }

  .user-input textarea {
    flex: 1;
    margin-right: 1rem;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 0.25rem;
    max-height: 200px;
    resize: none;
    width: 100%;
  }

  .user-input button {
    padding: 0.5rem 1rem;
  }


</style>
