<script>
  export let conversation = [];
</script>

<ul class="conversation">
  {#each conversation as message}
    <li class:is-user={message.isUser}>
      {message.text}
    </li>
  {/each}
</ul>

<style>
  .conversation {
    flex: 1;
    list-style: none;
    margin: 0;
    padding: 0;
    overflow-y: auto;
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
</style>