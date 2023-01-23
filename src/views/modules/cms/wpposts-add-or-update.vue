<template>
  <el-dialog :visible.sync="visible" :title="!dataForm.id ? $t('add') : $t('update')" :close-on-click-modal="false" :close-on-press-escape="false">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmitHandle()" :label-width="$i18n.locale === 'en-US' ? '120px' : '80px'">
          <el-form-item label="作者ID" prop="postAuthor">
          <el-input v-model="dataForm.postAuthor" placeholder="作者ID"></el-input>
      </el-form-item>
          <el-form-item label="发布时间" prop="postDate">
          <el-input v-model="dataForm.postDate" placeholder="发布时间"></el-input>
      </el-form-item>
          <el-form-item label="发布时间GMT" prop="postDateGmt">
          <el-input v-model="dataForm.postDateGmt" placeholder="发布时间GMT"></el-input>
      </el-form-item>
          <el-form-item label="帖子内容" prop="postContent">
          <el-input v-model="dataForm.postContent" placeholder="帖子内容"></el-input>
      </el-form-item>
          <el-form-item label="标题" prop="postTitle">
          <el-input v-model="dataForm.postTitle" placeholder="标题"></el-input>
      </el-form-item>
          <el-form-item label="摘要" prop="postExcerpt">
          <el-input v-model="dataForm.postExcerpt" placeholder="摘要"></el-input>
      </el-form-item>
          <el-form-item label="状态" prop="postStatus">
          <el-input v-model="dataForm.postStatus" placeholder="状态"></el-input>
      </el-form-item>
          <el-form-item label="评论状态" prop="commentStatus">
          <el-input v-model="dataForm.commentStatus" placeholder="评论状态"></el-input>
      </el-form-item>
          <el-form-item label="允许ping" prop="pingStatus">
          <el-input v-model="dataForm.pingStatus" placeholder="允许ping"></el-input>
      </el-form-item>
          <el-form-item label="帖子密码" prop="postPassword">
          <el-input v-model="dataForm.postPassword" placeholder="帖子密码"></el-input>
      </el-form-item>
          <el-form-item label="帖子名称" prop="postName">
          <el-input v-model="dataForm.postName" placeholder="帖子名称"></el-input>
      </el-form-item>
          <el-form-item label="to_ping" prop="toPing">
          <el-input v-model="dataForm.toPing" placeholder="to_ping"></el-input>
      </el-form-item>
          <el-form-item label="pingback记录" prop="pinged">
          <el-input v-model="dataForm.pinged" placeholder="pingback记录"></el-input>
      </el-form-item>
          <el-form-item label="修改时间" prop="postModified">
          <el-input v-model="dataForm.postModified" placeholder="修改时间"></el-input>
      </el-form-item>
          <el-form-item label="修改GMT时间" prop="postModifiedGmt">
          <el-input v-model="dataForm.postModifiedGmt" placeholder="修改GMT时间"></el-input>
      </el-form-item>
          <el-form-item label="内容过滤" prop="postContentFiltered">
          <el-input v-model="dataForm.postContentFiltered" placeholder="内容过滤"></el-input>
      </el-form-item>
          <el-form-item label="父帖子" prop="postParent">
          <el-input v-model="dataForm.postParent" placeholder="父帖子"></el-input>
      </el-form-item>
          <el-form-item label="原始链接" prop="guid">
          <el-input v-model="dataForm.guid" placeholder="原始链接"></el-input>
      </el-form-item>
          <el-form-item label="排序" prop="menuOrder">
          <el-input v-model="dataForm.menuOrder" placeholder="排序"></el-input>
      </el-form-item>
          <el-form-item label="帖子类型" prop="postType">
          <el-input v-model="dataForm.postType" placeholder="帖子类型"></el-input>
      </el-form-item>
          <el-form-item label="MIME类型" prop="postMimeType">
          <el-input v-model="dataForm.postMimeType" placeholder="MIME类型"></el-input>
      </el-form-item>
          <el-form-item label="评论总数" prop="commentCount">
          <el-input v-model="dataForm.commentCount" placeholder="评论总数"></el-input>
      </el-form-item>
      </el-form>
    <template slot="footer">
      <el-button @click="visible = false">{{ $t('cancel') }}</el-button>
      <el-button type="primary" @click="dataFormSubmitHandle()">{{ $t('confirm') }}</el-button>
    </template>
  </el-dialog>
</template>

<script>
import debounce from 'lodash/debounce'
export default {
  data () {
    return {
      visible: false,
      dataForm: {
        id: '',
        postAuthor: '',
        postDate: '',
        postDateGmt: '',
        postContent: '',
        postTitle: '',
        postExcerpt: '',
        postStatus: '',
        commentStatus: '',
        pingStatus: '',
        postPassword: '',
        postName: '',
        toPing: '',
        pinged: '',
        postModified: '',
        postModifiedGmt: '',
        postContentFiltered: '',
        postParent: '',
        guid: '',
        menuOrder: '',
        postType: '',
        postMimeType: '',
        commentCount: ''
      }
    }
  },
  computed: {
    dataRule () {
      return {
        postAuthor: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        postDate: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        postDateGmt: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        postContent: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        postTitle: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        postExcerpt: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        postStatus: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        commentStatus: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        pingStatus: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        postPassword: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        postName: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        toPing: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        pinged: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        postModified: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        postModifiedGmt: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        postContentFiltered: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        postParent: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        guid: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        menuOrder: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        postType: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        postMimeType: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        commentCount: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    init () {
      this.visible = true
      this.$nextTick(() => {
        this.$refs['dataForm'].resetFields()
        if (this.dataForm.id) {
          this.getInfo()
        }
      })
    },
    // 获取信息
    getInfo () {
      this.$http.get(`/cms/wpposts/${this.dataForm.id}`).then(({ data: res }) => {
        if (res.code !== 0) {
          return this.$message.error(res.msg)
        }
        this.dataForm = {
          ...this.dataForm,
          ...res.data
        }
      }).catch(() => {})
    },
    // 表单提交
    dataFormSubmitHandle: debounce(function () {
      this.$refs['dataForm'].validate((valid) => {
        if (!valid) {
          return false
        }
        this.$http[!this.dataForm.id ? 'post' : 'put']('/cms/wpposts/', this.dataForm).then(({ data: res }) => {
          if (res.code !== 0) {
            return this.$message.error(res.msg)
          }
          this.$message({
            message: this.$t('prompt.success'),
            type: 'success',
            duration: 500,
            onClose: () => {
              this.visible = false
              this.$emit('refreshDataList')
            }
          })
        }).catch(() => {})
      })
    }, 1000, { 'leading': true, 'trailing': false })
  }
}
</script>
