<script lang="ts">
    import { activeMenu, aboutContent, activeFooter } from "../../stores";
    import Button from "../atoms/Button.svelte";

    import CloseIcon from "../atoms/icons/CloseIcon.svelte";
    import Link from "../atoms/Link.svelte";

    let menuIsActive: Boolean;
    activeMenu.subscribe(value => menuIsActive = value);

    const activateFooter = () => {
        activeFooter.set(true);
        activeMenu.set(false);
    }

    const closeMenu = () => {
        activeMenu.set(false);
    }

    const setIntro = () => {
        activeMenu.set(false);
        aboutContent.set('intro');
    }

</script>

    <section class="overlay" class:visible={ menuIsActive }>
        <Button on:click={closeMenu} btnClass='btnClose' btnText=''>
            <CloseIcon />
        </Button>
        <div class="wrapper">
            <Link target='' on:click={closeMenu} linkDescription='Andas' linkPath='/'/>
            <Link target='' on:click={setIntro} linkDescription='Andas rätt' linkPath='/andasratt'/>
            <Link target='' on:click={activateFooter} linkDescription='Avslappningsljud' linkPath=''/>
            <Link target='' on:click={closeMenu} linkDescription='Om sidan' linkPath='/omsidan'/>
        </div>
    </section>

<style lang="scss">

    .overlay {
        background-color: var(--color-psi);
        width: 100%;
        position: fixed;
        top: 0;
        bottom: 0;
        z-index: 14;
        transform: translateX(-100%);
        overflow-y: auto;
        transition: transform .3s ease-in-out;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .visible {
        transform: translate(0);
    }

    .wrapper {
        margin-top: 5rem;
        display: flex;
        flex-direction: column;
        gap: 2rem;
        text-align: center;
    }

    .wrapper :global(a) {
        font-family: 'Caveat', cursive;
        text-decoration: none;
        font-size: 36px;
        font-weight: 600;
    }

    :global(.btnClose) {
        align-self: flex-start;
        padding-left: var(--padding-large);
        padding-top: var(--padding-large);
    }

</style>