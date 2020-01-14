<!-- 
    Can be used like this
    <Input 
        bind:value={value}
        {...props}>
    where props = {
        id,
        name,
        optional,
        valid,
        errorMessage,
        validation = {
            validate: (ev) => { after blur },
            validateKeyUp: (ev) => { after keyup, I used it only when valid === false for instant feedback },
        }
    } 
 -->

<script>
import { fade } from 'svelte/transition';

export let value;

export let type = 'text';
export let id;
export let name;
export let optional;
export let valid;
export let errorMessage;
export let validation;

const handleInput = (e) => {
    // in here, you can switch on type and implement
    // whatever behaviour you need
    value = type.match(/^(number|range)$/)
        ? +e.target.value
        : e.target.value;
};
</script>

<label for="{id}">{name}{#if !optional}*{/if}</label>
<input
    {type}
    id={id}
    placeholder={name}
    on:input={handleInput}
    on:blur={validation.validate}
    on:keyup={validation.validateKeyUp}
    class:error={valid === false}
    required>
{#if valid === false && !optional}
<label for={id} class="error" transition:fade>
    {@html errorMessage}
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
label.error{
    margin-top: -20px;
}
</style>
