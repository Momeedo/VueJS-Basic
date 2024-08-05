<template>
    <div>
        Selected Keywords from Child: {{ propFromParent }}
    </div>

</template>

<script>
export default {
    props: {
        propFromParent: {
            type: Array,
            required: true,
            default: () => []
        }
    },
    //props: ["propFromParent"],

}
</script>