<template>
<div class="row">
  <div class="col-md-2"></div>
  <div class="col-md-8">
    <div class="box box-solid">
      <div class="box-header">
        <div class="text-center registry-title">
          <h3 class="box-title">重置密码</h3>
        </div>
      </div>

      <div class="box-body">
        <div class="row row-margin-bottom">
          <div class="col-md-12">
            <Step>
              <StepItem index="1" name="验证账户" width="33" :is-active="stepId == 1" />
              <StepItem index="2" name="安全验证" width="33" :is-active="stepId == 2" />
              <StepItem index="3" name="重置密码" width="33" :is-active="stepId == 3" />
            </Step>
          </div>
        </div>

        <div class="row">
          <div class="col-md-12">
            <ValidAccount v-if="stepId == 1"/>
            <ValidEmail v-if="stepId == 2"/>
            <RestPassword v-if="stepId == 3"/>
          </div>
        </div>
      </div>
      <div class="box-footer">
        <div class="row">
          <div class="col-md-12">
            <div class="col-md-4"></div>
            <div class="col-md-2" v-if="stepId < maxStep">
              <button type="button" class="btn btn-block btn-primary"  @click="nextStep">
                下一步
              </button>
            </div>
            <div class="col-md-2" v-if="stepId == maxStep">
              <button type="button" class="btn btn-block btn-primary" @click="submit">
                保 存
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>
import Step from '../step/Step'
import StepItem from '../step/StepItem'
import ValidAccount from './ValidAccount'
import ValidEmail from './ValidEmail'
import RestPassword from './RestPassword'

export default {
  components: {
    Step,
    StepItem,
    ValidAccount,
    ValidEmail,
    RestPassword
  },
  data: function () {
    return {
      stepId: 1,
      maxStep: 3
    }
  },
  methods: {
    lastStep () {
      if (this.stepId > 1) {
        this.stepId = this.stepId - 1
      }
    },
    nextStep () {
      if (this.stepId < this.maxStep) {
        this.stepId = this.stepId + 1
      }
    },
    argee () {
    },
    submit () {
      this.$notify.info('提交成功，请等待工作人员审核')
    }
  }
}
</script>
