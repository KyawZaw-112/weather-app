<script>
import { useDark,useToggle } from '@vueuse/core'

const isDark = useDark({
    selector: 'body',
    attribute: 'color-scheme',
    valueDark: 'dark',
    valueLight: 'light',
})
const toggleDark = useToggle(isDark)
</script>

<template>
    <div>
        <button @click="toggleDark()">Click</button>
    </div>
</template>