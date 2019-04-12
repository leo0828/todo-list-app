<template>
  <Page class="page">
    <ActionBar title="备忘录" class="action-bar" />

    <TabView height="100%" selectedTabTextColor="#53ba82" tabTextFontSize="15">
      <TabViewItem title="待办事项">
        <StackLayout orientation="vertical" width="100%" height="100%">

          <GridLayout columns="2*,*" rows="*" width="100%" height="25%">
            <TextField col="0" row="0" v-model="textFieldValue" hint="新建待办事项..." editable="true"
              @returnPress="onButtonTap" />
            <Button col="1" row="0" text="创建" @tap="onButtonTap" />
          </GridLayout>

          <ListView separatorColor="transparent" class="list-group" for="todo in todos" @itemTap="onItemTap"
            style="height:75%">
            <v-template>
              <Label id="active-task" :text="todo.name" class="list-group-item-heading" />
            </v-template>
          </ListView>
        </StackLayout>
      </TabViewItem>
      <TabViewItem title="已办事项">
        <ListView separatorColor="transparent" class="list-group" for="done in dones" @itemTap="onDoneTap"
          style="height:75%">
          <v-template>
            <Label id="completed-task" :text="done.name" class="list-group-item-heading" />
          </v-template>
        </ListView>
      </TabViewItem>
    </TabView>
  </Page>
</template>

<script>
  export default {
    methods: {
      onItemTap: function (args) {
        action("操作", "取消", ["标记为已办事项", "删除"]).then(result => {
          console.log(result);
          switch (result) {
            case "标记为已办事项":
              this.dones.unshift(args.item);
              this.todos.splice(args.index, 1);
              break;
            case "删除":
              this.todos.splice(args.index, 1);
              break;
            default:
              break;
          }
        });
      },

      onDoneTap: function (args) {
        action("操作", "取消", ["标记为待办事项", "删除"]).then(result => {
          console.log(result);
          switch (result) {
            case "标记为待办事项":
              this.todos.unshift(args.item);
              this.dones.splice(args.index, 1);
              break;
            case "删除":
              this.dones.splice(args.index, 1);
              break;
            default:
              break;
          }
        });
      },

      onButtonTap() {
        console.log("New task added: " + this.textFieldValue + ".");
        this.todos.unshift({
          name: this.textFieldValue
        });
        this.textFieldValue = "";
      }
    },

    data() {
      return {
        dones: [],
        todos: [],
        textFieldValue: ""
      };
    }
  };
</script>

<style scoped>
  TextField {
    font-size: 20;
    color: #53ba82;
    margin-top: 10;
    margin-bottom: 10;
    margin-right: 5;
    margin-left: 20;
  }

  button {
    font-size: 20;
    font-weight: bold;
    color: white;
    background-color: #53ba82;
    height: 40;
    margin-top: 10;
    margin-bottom: 10;
    margin-right: 10;
    margin-left: 10;
    border-radius: 20px;
  }

  .home-panel {
    vertical-align: center;
    font-size: 20;
    margin: 15;
  }

  .description-label {
    margin-bottom: 15;
  }

  #active-task {
    font-size: 20;
    font-weight: bold;
    color: #53ba82;
    margin-left: 20;
    padding-top: 5;
    padding-bottom: 10;
  }

  #completed-task {
    font-size: 20;
    color: #d3d3d3;
    margin-left: 20;
    padding-top: 5;
    padding-bottom: 10;
    text-decoration: line-through;
  }
</style>