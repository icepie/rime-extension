<script setup lang="ts">
import { useToggle } from '@vueuse/core'
import 'uno.css'

const [show, toggle] = useToggle(false)

// 找到所有的输入框

// 为每个输入框添加一个监听事件

// 遍历dom

// 当dom 出现输入框时添加一个监听事件

// 监听页面刷新
// window.addEventListener('load', () => {
//   const inputList = document.querySelectorAll('input')

//   inputList.forEach((input) => {
//     input.addEventListener('focus', () => {
//       toggle()
//     })
//     input.addEventListener('blur', () => {
//       toggle()
//     })
//   })
// })

// console.log('asd')

// // onLoad(() => {
// const inputList = document.querySelectorAll('input')

// inputList.forEach((input) => {
//   console.log(input)

//   input.addEventListener('focus', () => {
//     toggle()
//   })
//   input.addEventListener('blur', () => {
//     toggle()
//   })
// })
// })

// 使用MutationObserver

onMounted(() => {
  const observer = new MutationObserver((mutationsList) => {
    for (const mutation of mutationsList) {
      if (mutation.type === 'childList') {
        const inputList = document.querySelectorAll('input,textarea,[contenteditable="true"]')

        inputList.forEach((input) => {
          // 判断事件是否已经绑定
          if (input.getAttribute('rime-event') === 'true')
            return

          input.addEventListener('focus', () => {
            // console.log('focus')

            toggle()
          })

          input.addEventListener('blur', () => {
            // console.log('blur')

            toggle()
          })

          input.setAttribute('rime-event', 'true')
        })
      }
    }
  })

  observer.observe(document.body, {
    childList: true,
    subtree: true,
    attributes: true,
  })
})
</script>

<template>
  <div class="fixed right-0 bottom-0 m-5 z-100 flex items-end font-sans select-none leading-1em">
    <div
      class="bg-white text-gray-800 rounded-lg shadow w-max h-min"
      p="x-4 y-2"
      m="y-auto r-2"
      transition="opacity duration-300"
      :class="show ? 'opacity-100' : 'opacity-0'"
    >
      <h1 class="text-lg">
        输入法demo
      </h1>
      <SharedSubtitle />
    </div>
    <button
      class="flex w-10 h-10 rounded-full shadow cursor-pointer border-none"
      bg="teal-600 hover:teal-700"
      @click="toggle()"
    >
      <pixelarticons-power class="block m-auto text-white text-lg" />
    </button>
  </div>
</template>
