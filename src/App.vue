<template>
  <div id="app">
    <Treeform :folder = "trees" :select = "select"></Treeform>
  </div>
</template>

<script>
import Treeform from './components/TreeList'

export default {
  name: 'App',
  components: {
    Treeform
  },
  data () {
    return {
      trees: [
        {
          label: '1级目录5',
          show: false,
          children: [
            {
              label: '5.1目录',
              show: false,
              children: [
                {
                  label: '5.1.1目录'
                },
                {
                  label: '5.1.2目录',
                  show: false,
                  children: [
                    {
                      label: '5.1.2.1目录'
                    }
                  ]
                }
              ]
            },
            {
              label: '5.2目录',
              show: false
            }
          ]
        }
      ]
    }
  },
  methods: {
    select (data) {
      console.log(data)
      data.show = !data.show
    }
  }
}
</script>

<style>
body,html{
  user-select: none;
}
</style>
