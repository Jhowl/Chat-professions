<script>
	import { createEventDispatcher } from 'svelte';
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
      on:keydown={e => {
        if (e.key === 'Enter') {
          sendMessage();
        }
      }}
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
    background-color: #eee;
    width: 100%;
  }

  .user-input textarea {
    flex: 1;
    border: 2px solid #ccc;
    border-radius: 0.25rem;
    width: 100%;
    height: 200px;
    padding: 0.5rem;
    margin: 0;
    font-size: 19px;
  }

  .user-input button {
    margin-top: 10px;
    padding: 0.5rem 1rem;
    width: 100%;
  }


</style>
