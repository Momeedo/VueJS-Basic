<template>
    <div>
        <input type="text" placeholder="Value to Emit" @input="$emit('change', $event.target.value)" />
    </div>

</template>

<script>
export default {
    emits: ["change"],
}
</script>