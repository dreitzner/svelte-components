<!-- 
    Can be used like this
    <Select bind:select={props}>
    where props = {
        id,
        name,
        value,
        valid: null,
        options: [{
            id,
            name,
        },
        ...],
        errorMessage,
    }
 -->

<script>
import { fade } from 'svelte/transition';

export let select;

$: select.valid = !!select.value.length
    || (select.valid === null
        ? null
        : select.valid);
</script>

<label for="{select.id}">{select.name}*</label>
<select
    name="{select.id}"
    id="{select.id}"
    bind:value={select.value}
    class:error={select.valid === false}
    required>
    <option value="" disabled selected>Choose {select.name}...</option>
    {#each select.options as option}
        <option value={option.id}>
            {option.name}
        </option>
    {/each}
</select>
{#if select.valid === false}
<label for="{select.id}" class="error" transition:fade>
    {@html select.errorMessage}
</label>
{/if}

<style>
select{
    margin-bottom: 20px;
    height: 40px;
    border: 1px solid #ccc;
    border-radius: 4px;
    font-size: 14px;
    padding: 10px;
}

option:disabled {
    display: none;
}
</style>
