<script context="module">
  const fn = "[name].svelte";

  /** @type {import('./__types/[slug]').Load} */
  export async function load({ params, fetch, session, stuff }) {
    const url = `https://api.reddit.com/r/${params.name}.json`;
    console.log(`${fn}: ${params.name}`);
    const response = await fetch(url);

    if (response.ok) {
      return {
        props: {
          posts: response.ok && (await response.json()).data.children,
        },
      };
    }

    return {
      status: response.status,
      error: new Error(`Could not load ${url}`),
    };
  }
</script>

<script>
  export let posts;
</script>

{#each posts as post}
  <div class="post">
    <a href={`https://reddit.com/${post.data.permalink}`} target="_blank" rel="noopener noreferrer">
      <h4>{post.data.title}</h4>
      {#if post.data.secure_media}
        <!-- display video -->
        {#if post.data.secure_media.reddit_video && post.data.secure_media.reddit_video.is_gif}
          <video controls muted autoplay loop src={post.data.secure_media.reddit_video.fallback_url} />
        {/if}
      {:else if post.data.post_hint === "image"}
        <img alt={post.data.title} src={post.data.url} />
      {/if}
    </a>
  </div>
{/each}

<style>
  .post {
    outline: 2px solid rgb(119, 138, 35);
    padding: 1rem;
    margin: 1rem;
  }
  video,
  img {
    width: 100%;
  }
</style>
