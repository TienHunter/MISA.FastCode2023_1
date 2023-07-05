<template>
  <div class="page">
    <div class="discuss-list__contaimer flex-1 flex flex-col">
      <div class="discuss-list__header flex justify-between items-center py-6">
        <div class="discuss-list-header__left">Thảo luận/ Hỏi đáp</div>
        <div class="discuss-list-header__right">
          <div
            class="btn btn--pri btn-add-discuss flex items-center"
            @click="isShowDetail = true">
            <div class="icon flex items-center w-6 h-6 icon-20 icon--add"></div>
            Thêm thảo luận/ câu hỏi
          </div>
        </div>
      </div>
      <div class="discuss-list__body flex-1 px-4">
        <div
          class="discuss-list-body__toolbars flex items-center justify-between">
          <div class="toolbars__left">
            <div class="toolbars-left__search">
              <BaseTexfield />
            </div>
          </div>
          <div class="toolbars__right">
            <div class="toolbars-right__refresh">
              <div class="icon-wrapper icon--refresh icon"></div>
            </div>
          </div>
        </div>
        <div class="discuss-body__content py-6">
          <div class="discuss-body__list">
            <div
              v-for="(item, index) in discussList"
              :key="index"
              class="dicuss-body__item pointer">
              <div class="flex items-center justify-start">
                <div class="discuss-item__left">
                  <div
                    class="discuss-item-left__icon icon-wrapper icon w-12 h-12"
                    :class="{
                      'icon--question':
                        item?.ThreadType === MISAEnum.SUBJECT_TYPE.QUESTION,
                      'icon--discuss':
                        item?.ThreadType === MISAEnum.SUBJECT_TYPE.DISCUSS,
                      'icon--share':
                        item?.ThreadType === MISAEnum.SUBJECT_TYPE.SHARE,
                    }"></div>
                </div>
                <div
                  class="discuss-item__right flex-1 flex flex-col justify-between">
                  <div class="discuss-item-right__title thread-item__title">
                    {{ item?.ThreadName }}
                  </div>
                  <div class="discuss-item-rigth__content flex items-center">
                    <div class="discuss-right-content__author mr-3">
                      {{ item?.ThreadUser }}
                    </div>
                    <div class="discuss-right-content__answers">
                      Đã trả lời :
                      {{ item?.AnswerNumber }}
                    </div>
                  </div>
                </div>
              </div>
              <div class="mt-2 horizontal-border"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <DiscussDetail v-if="isShowDetail" @closeDetail="isShowDetail = false" />
  </div>
  <!-- <DisscusForm></DisscusForm> -->
</template>
<script>
import MISAEnum from "@/helpers/enum";
import BaseTexfield from "../../components/base/textfield/BaseTexfield.vue";
import DiscussDetail from "./DiscussDetail/DiscussDetail.vue";
import { ref, onMounted, onBeforeMount } from "vue";
export default {
  name: "DiscussList",
  components: {
    BaseTexfield,
    DiscussDetail,
  },

  setup() {
    const isShowDetail = ref(false);
    const discussList = ref([]);
    onBeforeMount(() => {
      /// call api
      discussList.value = [
        {
          ThreadId: 1,
          ThreadName: "Cần giúp đỡ về việc sử dụng thuộc tính flex?",
          ThreadType: 1,
          ThreadUser: "Nguyễn Văn Mạnh",
          AnswerNumber: 100,
          CreatedDate: "",
        },
        {
          ThreadId: 2,
          ThreadName: "Có bao nhiêu cách để thực hiện layout website?",
          ThreadType: 1,
          ThreadUser: "Đỗ Văn Cường",
          AnswerNumber: 8,
          CreatedDate: "",
        },
        {
          ThreadId: 3,
          ThreadName:
            "Thảo luận về hiệu năng sử dụng các component có binding 2 chiều với nhiều thông tin.",
          ThreadType: 2,
          ThreadUser: "Nguyễn Thị Nga",
          AnswerNumber: 12,
          CreatedDate: "",
        },
        {
          ThreadId: 4,
          ThreadName:
            "Chia sẻ việc lập trình đồng bộ trong Javascript, những điều cần lưu ý.",
          ThreadType: 3,
          ThreadUser: "Hoàng Ngọc Hân",
          AnswerNumber: 54,
          CreatedDate: "",
        },
        {
          ThreadId: 5,
          ThreadName: "Cho em hỏi về đồ án tốt nghiệp tại trường ĐH Bách Khoa.",
          ThreadType: 1,
          ThreadUser: "Trần Diễm Giang",
          AnswerNumber: 20,
          CreatedDate: "",
        },
      ];
    });
    onMounted(() => {});
    return {
      discussList,
      isShowDetail,
      MISAEnum,
    };
  },
  //   created() {
  //     // fetch('data/threads.json')
  //     //     .then((response) => response.json())
  //     //     .then((json) => console.log(json));
  //   },
  //   data() {
  //     return {
  //       data: [
  //         {
  //           ThreadId: 1,
  //           ThreadName: "Cần giúp đỡ về việc sử dụng thuộc tính flex?",
  //           ThreadType: 1,
  //           ThreadUser: "Nguyễn Văn Mạnh",
  //           AnswerNumber: 100,
  //           CreatedDate: "",
  //         },
  //         {
  //           ThreadId: 2,
  //           ThreadName: "Có bao nhiêu cách để thực hiện layout website?",
  //           ThreadType: 1,
  //           ThreadUser: "Đỗ Văn Cường",
  //           AnswerNumber: 8,
  //           CreatedDate: "",
  //         },
  //         {
  //           ThreadId: 3,
  //           ThreadName:
  //             "Thảo luận về hiệu năng sử dụng các component có binding 2 chiều với nhiều thông tin.",
  //           ThreadType: 2,
  //           ThreadUser: "Nguyễn Thị Nga",
  //           AnswerNumber: 12,
  //           CreatedDate: "",
  //         },
  //         {
  //           ThreadId: 4,
  //           ThreadName:
  //             "Chia sẻ việc lập trình đồng bộ trong Javascript, những điều cần lưu ý.",
  //           ThreadType: 3,
  //           ThreadUser: "Hoàng Ngọc Hân",
  //           AnswerNumber: 54,
  //           CreatedDate: "",
  //         },
  //         {
  //           ThreadId: 5,
  //           ThreadName: "Cho em hỏi về đồ án tốt nghiệp tại trường ĐH Bách Khoa.",
  //           ThreadType: 1,
  //           ThreadUser: "Trần Diễm Giang",
  //           AnswerNumber: 20,
  //           CreatedDate: "",
  //         },
  //       ],
  //     };
  //   },
};
</script>
<style scoped>
@import url(./DiscussList.css);
.page__container {
  padding: 16px;
}

.thread-list {
  display: flex;
  flex-direction: column;
  margin-top: 10px;
}

.thread__icon {
  width: 40px;
  height: 40px;
  background-size: 40px;
  border-radius: 50%;
  flex: 0 0 40px;
  background-repeat: no-repeat;
  background-position: center;
}

.thread-item {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  column-gap: 10px;
  padding: 10px 0;
}

.thread-item + .thread-item {
  border-top: 1px solid var(--border-color-default);
}

.thread-item__title {
  font-weight: 700;
  color: var(--color-primary);
  line-height: 20px;
}

.thread-item__info {
  display: flex;
  align-items: center;
  column-gap: 16px;
  margin-top: 4px;
  font-size: 12px;
}
.discuss-list__body {
  background-color: #fff;
}
</style>
