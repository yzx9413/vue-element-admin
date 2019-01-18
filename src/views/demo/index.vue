<template>
  <div>
    <el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick"></el-tree>
  </div>
</template>
<script>
export default {
  name: "demo",
  data() {
    return {
      data: [
        {
          label: "部门1",
          children: [
            {
              label: "二级部门 1-1",
              children: [
                {
                  label: "三级部门 1-1-1",
                  children: [
                    {
                      label: "四级部门 1-1-1"
                    }
                  ]
                }
              ]
            }
          ]
        },
        {
          label: "部门2",
          children: [
            {
              label: "二级部门 2-1",
              children: [
                {
                  label: "三级部门 2-1-1"
                }
              ]
            },
            {
              label: "二级部门 2-2",
              children: [
                {
                  label: "三级部门 2-2-1"
                }
              ]
            }
          ]
        },
        {
          label: "部门3",
          children: [
            {
              label: "二级部门 3-1",
              children: [
                {
                  label: "三级部门 3-1-1"
                }
              ]
            },
            {
              label: "二级部门 3-2",
              children: [
                {
                  label: "三级部门 3-2-1"
                }
              ]
            }
          ]
        }
      ],
      defaultProps: {
        children: "children",
        label: "label"
      }
    };
  },
  methods: {
    handleNodeClick(data) {
      console.log(data);
    }
  }
};
</script>
<style scoped>
</style>
