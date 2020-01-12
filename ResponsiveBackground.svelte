<!-- 
    Can be used like this
    <ResponsiveBackground 
        {images}
        {fallbackImage}>
        some optional html
    </ResponsiveBackground>
    
    where images = [
        { media, type, srcset }
    ]
    and where fallbackImage = {
        src,
        alt,
    }
 -->

<script>
  export let images;
  export let fallbackImage;
  const {src, alt} = fallbackImage;

  let curSrc;
  const updateBg = ev => {
    const img = ev.target;
    var src = typeof img.currentSrc !== "undefined" ? img.currentSrc : img.src;
    if (curSrc !== src) {
      curSrc = `url(${src})`;
    }
  };
</script>

<div style="background-image: {curSrc};">
  <picture>
    {#each images as {media, srcset, type}}
		<source
			{media}
			{srcset}
			{type} />
    {/each}
    <img
		on:load={updateBg}
		{src}
		{alt} />
  </picture>
  <slot></slot>
</div>

<style>
  picture,
  picture img {
    visibility: hidden;
    width: 0;
    height: 0;
    overflow: hidden;
  }

  div {
    overflow: hidden;
    position: relative;
    display: block;
    background-position: center;
    background-size: cover;
    background-color: #c87f3a;
  }
</style>
