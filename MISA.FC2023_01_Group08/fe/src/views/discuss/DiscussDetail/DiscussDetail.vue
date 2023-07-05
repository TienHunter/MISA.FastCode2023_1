<template>
  <div class="m-form">
    <div class="m-form-container">
      <div class="m-form__header flex items-center justif-between">
        <div class="form-header__title">Thông tin chủ để</div>
        <div class="form-header__close"></div>
      </div>
      <div class="m-form__body">
        <BaseTexfield
          v-model="discussDetail.author"
          classLabel="w-full mb-4"
          required
          label="Họ và tên"
          :err-msg="errsValidate?.author ?? ''"
          @empty-err-msg="
            () => {
              delete errsValidate.author;
            }
          " />
        <BaseTexfield
          v-model="discussDetail.title"
          classLabel="w-full mb-4"
          required
          label="Tiêu đề"
          :err-msg="errsValidate?.title ?? ''"
          @empty-err-msg="
            () => {
              delete errsValidate.title;
            }
          " />
        <div class="form-body__subjects mb-4">
          <label class=""
            >Loại chủ để
            <div class="flex items-center justify-between mt-2">
              <label class="flex items-center">
                <input
                  name="subjectType"
                  type="radio"
                  v-model="discussDetail.subjectType"
                  :value="MISAEnum.SUBJECT_TYPE.QUESTION" />
                Hỏi đáp
              </label>
              <label class="flex items-center">
                <input
                  name="subjectType"
                  type="radio"
                  v-model="discussDetail.subjectType"
                  :value="MISAEnum.SUBJECT_TYPE.DISCUSS" />
                Thảo luận
              </label>
              <label class="flex items-center">
                <input
                  name="subjectType"
                  type="radio"
                  v-model="discussDetail.subjectType"
                  :value="MISAEnum.SUBJECT_TYPE.SHARE" />
                Chia sẻ
              </label>
            </div>
          </label>
        </div>
        <div class="form-body__content">
          <textarea
            v-model="discussDetail.content"
            class="w-full"
            name=""
            id=""
            cols="30"
            rows="6"></textarea>
        </div>
      </div>
      <div class="m-form__footer">
        <div class="btn btn--sub" @click="onCancel">Hủy</div>
        <div class="btn btn--pri" @click="onSave">Lưu</div>
      </div>
    </div>
  </div>
</template>
<script>
import { ref } from "vue";
import MISAEnum from "../../../helpers/enum";
import BaseTexfield from "../../../components/base/textfield/BaseTexfield.vue";
export default {
  components: {
    BaseTexfield,
  },
  props: {
    isShow: {
      type: Boolean,
      default: false,
    },
  },
  emits: ["closeDetail"],
  setup(props, ctx) {
    const discussDetail = ref({});
    const errsValidate = ref({});
    const onCancel = () => {
      ctx.emit("closeDetail");
    };
    const onSave = () => {
      // ctx.emit("closeDetail");
      console.log(discussDetail.value);
    };
    const isValidate = () => {
      // xóa lỗi trước đó
      // Xóa tất cả các trường của reactive object
      Object.keys(errsValidate).forEach((key) => {
        delete errsValidate[key];
      });
      if (!discussDetail?.value?.author) {
        discussDetail.value.author = "Ản danh";
      }
      if (!discussDetail?.value?.title) {
        errsValidate.value.title = "Trường này không được để trống";
      }
      const isEmpty = Object.keys(errsValidate).length === 0;
      if (isEmpty) {
        // console.log("isEmpty", isEmpty);
        return true;
      }
    };
    const hanldeValidate = () => {
      if (isValidate) {
        // call api
      }
    };
    return {
      discussDetail,
      MISAEnum,
      onCancel,
      onSave,
      hanldeValidate,
      errsValidate,
    };
  },
};
</script>
<style lang=""></style>
