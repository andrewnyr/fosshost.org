<script lang="ts">
    import { fade } from 'svelte/transition';
    import Input from './Input.svelte';
    import * as yup from 'yup';

    export let data: FormResponse;
    export let validate: any;
    export let pageValidate: any;

    const validator = yup.object().shape({
        name: yup.string().required(),
        email: yup.string().required().email()
    })

    let errors = {
        name: null,
        email: null,
    }

</script>

<main in:fade={{delay: 0, duration: 400}}>
    <h1>Personal Information</h1>
    <p>Please note that we need your full name and contact detail in order to process your application.</p>
    <Input on:blur={() => {errors = validate(validator, 'name', data.personal, errors)}} error={errors.name} label="Full name" type="text" placeholder="What's your name" bind:value={data.personal.name} />
    <Input on:blur={() => {errors = validate(validator, 'email', data.personal, errors)}} error={errors.email} label="Email" type="email" placeholder="you@example.com" bind:value={data.personal.email} />
    <div class="buttons">
        <button class="submit" on:click={() => {errors = pageValidate(validator, data.personal, errors)}}>Next</button>
    </div>
</main>


<style>

</style>