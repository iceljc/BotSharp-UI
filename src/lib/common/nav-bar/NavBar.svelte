<script>

    /** @type {string} */
    export let id = "nav-bar";

    /** @type {string} */
    export let role = "tablist";

    /** @type {string} */
    export let containerClasses = "";

    /** @type {string} */
    export let containerStyles = "";

    /** @type {boolean} */
    export let disableDefaultStyles = false;
</script>

<ul
    class="nav nav-tabs {disableDefaultStyles ? '' : 'nav-tabs-default nav-container'} {containerClasses}"
    style={`${containerStyles}`}
    id={id}
    role={role}
>
    <slot />
</ul>

<style>
    .nav-container {
        height: 100%;
    }
</style>