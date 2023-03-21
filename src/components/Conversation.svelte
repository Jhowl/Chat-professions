<script>
  export let conversation = {
    messages: [],
    loading: false
  };
</script>

<ul class="conversation">
  {#each conversation.messages as message}
    <li class:is-user={message.isUser}>
      {message.text}
    </li>
  {/each}

  {#if conversation.loading}
    <li class="is-loading"></li>
  {/if}

</ul>

<style>
  .conversation {
    display: block;
    list-style: none;
    margin: 0;
    padding: 0;
    overflow-y: auto;
    width: 100%;
    height: 600px;
  }

  .conversation li {
    margin-bottom: 1rem;
    padding: 0.5rem;
    border-radius: 0.25rem;
    background-color: #eee;
    word-break: break-word;
  }

  .conversation li.is-user {
    display: block;
    background-color: #4794e7;
    color: white;
    text-align: right;
  }

  .conversation li.is-loading {
    position: relative;
    background-color: transparent;
  }

  .conversation li.is-loading::before {
    content: "loading...";
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    animation: loading 1s infinite;
    margin-bottom: 1rem;
    padding: 0.5rem;
    border-radius: 0.25rem;
    background-color: #eee;
    word-break: break-word;
  }

  @keyframes loading {
    0% {
      opacity: 0.2;
    }
    20% {
      opacity: 1;
    }
    100% {
      opacity: 0.2;
    }
  }
</style>
