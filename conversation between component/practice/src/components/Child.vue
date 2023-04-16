<template>
    <div>
        字數: {{ msgCount }}
    </div>
    <!-- {{ data }} -->
</template>

<script setup>
    import { computed } from '@vue/reactivity';
    import { watch } from 'vue'

    /*
        父傳子
    */

    // 兩種從父組件傳進來的方式: 陣列跟物件
    // const props = defineProps(['data'])

    const props = defineProps({
        data: {
            type: String,
            default: '',
            required: true,
        }
    })

    const msgCount = computed(() => {
        return props.data.length;
    })


    /*
        子傳父
    */
    // e.g. 當 msgCount 有變，就發送一個 update 事件
    const emit = defineEmits(['update']);

    watch(msgCount, (newValue, oldValue) => {
        emit('update', `from child: ${newValue}`)
    })

</script>