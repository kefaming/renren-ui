<template>
  <el-card shadow="never" class="aui-card--fill">
    <div class="mod-cms__wpposts}">
      <el-form :inline="true" :model="dataForm" @keyup.enter.native="getDataList()">
        <el-form-item>
          <el-input v-model="dataForm.id" placeholder="id" clearable></el-input>
        </el-form-item>
        <el-form-item>
          <el-button @click="getDataList()">{{ $t('query') }}</el-button>
        </el-form-item>
        <el-form-item>
          <el-button type="info" @click="exportHandle()">{{ $t('export') }}</el-button>
        </el-form-item>
        <el-form-item>
          <el-button v-if="$hasPermission('cms:wpposts:save')" type="primary" @click="addOrUpdateHandle()">{{ $t('add') }}</el-button>
        </el-form-item>
        <el-form-item>
          <el-button v-if="$hasPermission('cms:wpposts:delete')" type="danger" @click="deleteHandle()">{{ $t('deleteBatch') }}</el-button>
        </el-form-item>
      </el-form>
      <el-table v-loading="dataListLoading" :data="dataList" border @selection-change="dataListSelectionChangeHandle" style="width: 100%;">
        <el-table-column type="selection" header-align="center" align="center" width="50"></el-table-column>
        <el-table-column prop="id" label="ID" header-align="center" align="center"></el-table-column>
        <el-table-column prop="postAuthor" label="作者ID" header-align="center" align="center"></el-table-column>
        <el-table-column prop="postDate" label="发布时间" header-align="center" align="center"></el-table-column>
        <el-table-column prop="postDateGmt" label="发布时间GMT" header-align="center" align="center"></el-table-column>
        <el-table-column prop="postContent" label="帖子内容" header-align="center" align="center"></el-table-column>
        <el-table-column prop="postTitle" label="标题" header-align="center" align="center"></el-table-column>
        <el-table-column prop="postExcerpt" label="摘要" header-align="center" align="center"></el-table-column>
        <el-table-column prop="postStatus" label="状态" header-align="center" align="center"></el-table-column>
        <el-table-column prop="commentStatus" label="评论状态" header-align="center" align="center"></el-table-column>
        <el-table-column prop="pingStatus" label="允许ping" header-align="center" align="center"></el-table-column>
        <el-table-column prop="postPassword" label="帖子密码" header-align="center" align="center"></el-table-column>
        <el-table-column prop="postName" label="帖子名称" header-align="center" align="center"></el-table-column>
        <el-table-column prop="toPing" label="to_ping" header-align="center" align="center"></el-table-column>
        <el-table-column prop="pinged" label="pingback记录" header-align="center" align="center"></el-table-column>
        <el-table-column prop="postModified" label="修改时间" header-align="center" align="center"></el-table-column>
        <el-table-column prop="postModifiedGmt" label="修改GMT时间" header-align="center" align="center"></el-table-column>
        <el-table-column prop="postContentFiltered" label="内容过滤" header-align="center" align="center"></el-table-column>
        <el-table-column prop="postParent" label="父帖子" header-align="center" align="center"></el-table-column>
        <el-table-column prop="guid" label="原始链接" header-align="center" align="center"></el-table-column>
        <el-table-column prop="menuOrder" label="排序" header-align="center" align="center"></el-table-column>
        <el-table-column prop="postType" label="帖子类型" header-align="center" align="center"></el-table-column>
        <el-table-column prop="postMimeType" label="MIME类型" header-align="center" align="center"></el-table-column>
        <el-table-column prop="commentCount" label="评论总数" header-align="center" align="center"></el-table-column>
        <el-table-column :label="$t('handle')" fixed="right" header-align="center" align="center" width="150">
          <template slot-scope="scope">
            <el-button v-if="$hasPermission('cms:wpposts:update')" type="text" size="small" @click="addOrUpdateHandle(scope.row.id)">{{ $t('update') }}</el-button>
            <el-button v-if="$hasPermission('cms:wpposts:delete')" type="text" size="small" @click="deleteHandle(scope.row.id)">{{ $t('delete') }}</el-button>
          </template>
        </el-table-column>
      </el-table>
      <el-pagination
        :current-page="page"
        :page-sizes="[10, 20, 50, 100]"
        :page-size="limit"
        :total="total"
        layout="total, sizes, prev, pager, next, jumper"
        @size-change="pageSizeChangeHandle"
        @current-change="pageCurrentChangeHandle">
      </el-pagination>
      <!-- 弹窗, 新增 / 修改 -->
      <add-or-update v-if="addOrUpdateVisible" ref="addOrUpdate" @refreshDataList="getDataList"></add-or-update>
    </div>
  </el-card>
</template>

<script>
import mixinViewModule from '@/mixins/view-module'
import AddOrUpdate from './wpposts-add-or-update'
export default {
  mixins: [mixinViewModule],
  data () {
    return {
      mixinViewModuleOptions: {
        getDataListURL: '/cms/wpposts/page',
        getDataListIsPage: true,
        exportURL: '/cms/wpposts/export',
        deleteURL: '/cms/wpposts',
        deleteIsBatch: true
      },
      dataForm: {
        id: ''
      }
    }
  },
  components: {
    AddOrUpdate
  }
}
</script>
