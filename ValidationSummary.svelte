<!-- 
    VALIDATION SUMMARY
    - takes in an array of form errors with { id, errorMessage }
    - focuses the first element
 -->
<script>
import { afterUpdate } from 'svelte';
export let validationSummaryData;
let summaryEl;

afterUpdate(() => {
    if (!summaryEl) return;
    summaryEl.querySelector('li').focus();
});
</script>

{#if validationSummaryData.length}
<ul bind:this={summaryEl}>
    <div class="validationSummaryHeadline">The following errors occured:</div>
    {#each validationSummaryData as data}
    <li>
        <a href="#{data.props.id}">{data.props.errorMessage}</a>
    </li>
    {/each}
</ul>
{/if}

<style>
ul {
    border: 1px solid red;
    color: red;
    background: #fae3e5;
}
ul > * {
    padding: 5px 10px;
}
a {
    color: red;
}
</style>
