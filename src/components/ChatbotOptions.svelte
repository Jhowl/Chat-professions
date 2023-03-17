<script>
  import { createEventDispatcher, onMount } from 'svelte'
  import getChatbots from './getChatBots.js'
  const dispatch = createEventDispatcher();

  let chatbots = [];
  let currentChatbot = 'Bot 1';
  let isDropdownOpen = true;

  function changeChatbot(chatbot) {
    currentChatbot = chatbot.value;
    // dispatch('changeChatbot', chatbot);
    isDropdownOpen = false;
  }

  onMount(async () => {
    chatbots = getChatbots()
  });

</script>

<div class="chatbot-options">
  <h2>Chatbots</h2>
  <p>Select chatbot: <strong>{currentChatbot}</strong></p>

  <div class="select-container">
      <ul>
        {#each chatbots as chatbot}
          <li class="selected-value" on:click={() => changeChatbot(chatbot)} on:keydown={() => changeChatbot(chatbot)}>{chatbot.value}</li>
        {/each}
      </ul>
  </div>
</div>

<style>
  .chatbot-options {
    display: block;
    flex-direction: column;
    align-items: center;
    width: 40%;
    padding: 1rem;
    background-color: #eee;
    text-align: left;
  }

  .chatbot-options h2 {
    margin-top: 0;
  }

  .select-container {
    position: relative;
    width: 100%;
    cursor: pointer;
    align-items: center;
  }

  .select-container ul {
    padding: inherit;
  }

  .selected-value {
    display: block;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 0.25rem;
    background-color: #fff;
    text-align: center;
    margin-bottom: 10px;
  }

  .selected-value:hover {
    background-color: #eee;
  }
</style>
