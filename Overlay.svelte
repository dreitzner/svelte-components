<!-- 
    Can be used like this
    {#if showOverlay}
	<Overlay
		on:overlay={handleOverlay}>
        some html
    </Overlay>
    {/if}
 -->

<script>
import { createEventDispatcher } from 'svelte';
import { fly } from 'svelte/transition';
import svgClose from '../inline-svg/close.svg'; // I used 'rollup-plugin-svg' to inline my svg

const dispatch = createEventDispatcher();
const overlay = (ev) => {
    if(!ev.target.classList.contains("js-close")) return;
    dispatch("overlay", "close");
};
</script>

<div
    class="shadow js-close"
    on:click={overlay}>
    <div
        class="content"
        transition:fly="{{ y: 200, duration: 600 }}">
        <button class="js-close" title="close dialog">
            {@html svgClose}
        </button>
        <slot></slot>
    </div>
</div>

<style>
.shadow {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background: rgba(0, 0, 0, .9);
}

.content {
    position: relative;
    background: #fff;
    padding: 48px 56px 0;
    max-width: 730px;
    margin: 0 auto;
    height: 100%;
    overflow-y: auto;
    z-index: 5;
}
.content:after {
    content: '';
    display: block;
    padding-bottom: 56px;
}

button {
    position: absolute;
    top: 20px;
    right: 20px;
}
</style>
