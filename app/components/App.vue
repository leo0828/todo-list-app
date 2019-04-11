<template>
  <Page>
    <ActionBar
      title="My Tasks"
      android:flat="true"
    />
    <TabView
      android:tabBackgroundColor="#53ba82"
      android:tabTextColor="#c4ffdf"
      android:selectedTabTextColor="#ffffff"
      androidSelectedTabHighlightColor="#ffffff"
    >
      <TabViewItem title="TO DO">
        <!-- Positions an input field, a button, and the list of tasks in a vertical stack. -->
        <StackLayout orientation="vertical" width="100%" height="100%">

          <GridLayout columns="2*,*" rows="*" width="100%" height="25%">
            <!-- Configures the text field and ensures that pressing Return on the keyboard produces the same result as tapping the button. -->
            <TextField col="0" row="0" v-model="textFieldValue" hint="Type new task..." editable="true" @returnPress="onButtonTap" /> 

            <Button col="1" row="0" text="Add task" @tap="onButtonTap" />
          </GridLayout>

          <ListView class="list-group" for="todo in todos" @itemTap="onItemTap" style="height:75%">
            <v-template>
              <Label :text="todo.name" class="list-group-item-heading" />
            </v-template>
          </ListView>
        </StackLayout>
      </TabViewItem>
      <TabViewItem title="COMPLETED">
        <GridLayout
          columns="*"
          rows="*"
        >
          <Label
            class="message"
            :text="'Hello '+name"
            col="0"
            row="0"
          />
        </GridLayout>
      </TabViewItem>
    </TabView>
  </Page>
</template>

<script >
import { mapState } from "vuex";
export default {
  computed: {
    ...mapState(["name"])
  },
  data() {
    return {
      msg: "Hello World!"
    };
  }
};
</script>

<style scoped>
ActionBar {
  background-color: #53ba82;
  color: #ffffff;
}

.message {
  vertical-align: center;
  text-align: center;
  font-size: 20;
  color: #333333;
}
</style>
