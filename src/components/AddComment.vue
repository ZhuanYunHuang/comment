<template>
  <div class="addComment">
    <!-- 文本框 -->
    <textarea class="text" v-model="comment" :placeholder="tip"></textarea>
    <br />

    <button @click="add" v-show="!isActiveReply">添加评论</button>
    <!-- 若点击回复键，则添加评论按钮隐藏，显示回复和取消回复 -->
    <button @click="sureReply(currentIndex)" v-show="isActiveReply">
      回复
    </button>
    <button @click="quitReply" v-show="isActiveReply">取消回复</button>
    <!-- 遍历评论 -->
    <div v-for="(item, index) in messages" :key="index">
      <!-- 点击收起或展开评论 -->
      <div @click="active(index)" class="show">
        <span><img src="../assets/img/上.png" v-show="isActive[index]" /></span>
        <span
          ><img src="../assets/img/下.png" v-show="!isActive[index]"
        /></span>
        <span>用户{{ item.name }}:</span>
      </div>
      <div v-show="isActive[index]">
        <div>
          <span>{{ item.content }}</span
          ><span class="reply" @click="addReply(index)" style="margin-left: 5px"
            >回复</span
          >
        </div>
        <!-- 点击收起或展开回复 -->
        <div
          v-if="item.reply.length != 0"
          @click="showReply(index)"
          class="replyLine"
        >
          <span v-show="isReply[index]"
            >收起回复<img src="../assets/img/上.png"
          /></span>
          <span v-show="!isReply[index]"
            >点击展开{{ item.reply.length }}条回复<img
              src="../assets/img/下.png"
          /></span>
        </div>
        <div v-show="isReply[index]">
          <!-- 遍历回复 -->
          <div
            v-for="(items, indexs) in item.reply"
            :key="indexs"
            class="replyContent"
          >
            回复{{ items.replyName + 1 }}:{{ items.replyContent }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddComment",
  data() {
    return {
      messages: [], //用于存放评论的数组，里面含有名字，内容以及回复内容三个属性=>messages:[{name:'',content:'',reply:[]}]
      comment: "", //用于双向绑定文本框输入的内容
      isActive: [], //用于存放评论点击展开的数组
      isReply: [], //用于存放回复点击展开的数组
      isActiveReply: false,
      tip: "",
      currentIndex: 0,
    };
  },

  methods: {
    //添加评论
    add() {
      if (this.comment != "") {
        this.messages.push({
          name: this.messages.length,
          content: this.comment,
          reply: [],
        });
        this.comment = "";
        this.tip = "";
        this.isActive.push(true);
        this.isReply.push(true);
        console.log(this.messages);
      }
    },
    //点击展开或收起评论
    active(index) {
      this.isActive[index] = !this.isActive[index];
      console.log(this.isActive);
    },
    //点击展开或收起回复
    showReply(index) {
      this.isReply[index] = !this.isReply[index];
      console.log(this.isReply);
    },
    //点击添加回复
    addReply(index) {
      this.currentIndex = index;
      this.isActiveReply = true;
      this.tip = "回复用户" + this.messages[index].name + ":";
      console.log("回复用户" + index);
      console.log(this.messages[index].reply);
    },
    //添加回复确定
    sureReply(index) {
      if (this.comment != "") {
        this.messages[index].reply.push({
          replyName: this.messages[index].reply.length,
          replyContent: this.comment,
        });
        this.comment = "";
        this.tip = "";
        this.isActiveReply = !this.isActiveReply;
        console.log(index);
      }
    },
    //取消回复
    quitReply() {
      this.isActiveReply = false;
      this.tip = "";
    },
  },
};
</script>

<style scoped>
.text {
  width: 300px;
  height: 100px;
}
.reply {
  font-size: 12px;
  color: gray;
}
.replyContent {
  font-size: 12px;
}
.show {
  height: 30px;
  background-color: rgb(226, 226, 226);
  display: flex;
  align-items: center;
}
.show span {
  line-height: 30px;
}
img {
  width: 20px;
  margin-top: 5px;
}
.replyLine {
  font-size: 12px;
}
.replyLine img {
  width: 11px;
}
</style>