<!-- 
    Can be used like this
    <Select
        bind:value={value}
        {...props}>
    where props = {
        id,
        name,
        valid: null,
        options: [{
            id,
            name,
        },
        ...],
        errorMessage,
        validation = {
            validate: (ev) => { after on:change },
        }
    }
 -->

<script>
import { fade } from 'svelte/transition';

export let value;

export let id;
export let name;
export let valid;
export let options = [];
export let errorMessage;
export let validation;
</script>

<label for="{id}">{name}*</label>
<select
    name="{id}"
    id="{id}"
    bind:value={value}
    on:change={validation.validate}
    class:error={valid === false}
    required>
    <option value="" disabled selected>Choose {name}...</option>
    {#each options as option}
        <option value={option.id}>
            {option.name}
        </option>
    {/each}
</select>
{#if valid === false}
<label for="{id}" class="error" transition:fade>
    {@html errorMessage}
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
