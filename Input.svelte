<!-- 
    Can be used like this
    <Input 
        bind:input={props}
        {validation}>
    where props = {
        id,
        name,
        optional,
        valid,
        errorMessage,
    }
    and where validation = {
        validate: (ev) => { after blur },
        validateKeyUp: (ev) => { after keyup, I used it only when valid === false for instant feedback },
    }
 -->

<script>
import { fade } from 'svelte/transition';

export let input;
export let validation;

const type = input.type || 'text';

const handleInput = (e) => {
    // in here, you can switch on type and implement
    // whatever behaviour you need
    input.value = type.match(/^(number|range)$/)
        ? +e.target.value
        : e.target.value;
};
</script>

<label for="{input.id}">{input.name}{#if !input.optional}*{/if}</label>
<input
    {type}
    id={input.id}
    placeholder={input.name}
    on:input={handleInput}
    on:blur={validation.validate}
    on:keyup={validation.validateKeyUp}
    class:error={input.valid === false}
    required>
{#if input.valid === false && !input.optional}
<label for={input.id} class="error" transition:fade>
    {@html input.errorMessage}
</label>
{/if}

<style>
input {
    margin-bottom: 20px;
    height: 40px;
    border: 1px solid #ccc;
    border-radius: 4px;
    font-size: 14px;
    padding: 10px;
    width: 100%;
}
</style>
