<template>
  <div>
    <!-- 动漫列表展示 -->
    <el-table :data="tableData" stripe row-key="id">
      <el-table-column prop="cover" label="封面">
        <template v-slot="{ row }">
          <el-image style="width: 100px; height: 100px" :src="row.cover" fit="cover"></el-image>
        </template>
      </el-table-column>
      <el-table-column prop="name" label="动漫名称"></el-table-column>
      <el-table-column prop="description" label="描述"></el-table-column>
      <el-table-column prop="publishDate" label="上映时间"></el-table-column>
      <el-table-column prop="author" label="作者"></el-table-column>
      <el-table-column prop="publisher" label="发行公司"></el-table-column>
      <el-table-column prop="category" label="分类"></el-table-column>
      <el-table-column prop="bookNo" label="番号"></el-table-column>
    </el-table>

    <!-- 分页 -->
    <div style="margin-top: 20px">
      <el-pagination
          background
          :current-page.sync="params.pageNum"
          :page-size="params.pageSize"
          layout="prev, pager, next"
          @current-change="handleCurrentChange"
          :total="total">
      </el-pagination>
    </div>
  </div>
</template>

<script>
import request from "@/utils/request";

export default {
  name: 'AnimeListDisplay',
  data() {
    return {
      tableData: [],
      total: 0,
      params: {
        pageNum: 1,
        pageSize: 10
      }
    };
  },
  created() {
    this.fetchTableData();
  },
  methods: {
    fetchTableData() {
      request.get('/book/page', {
        params: this.params
      }).then(response => {
        if (response.code === '200') {
          this.tableData = response.data.list;
          this.total = response.data.total;
        } else {
          this.$message.error('Failed to load the list of anime.');
        }
      });
    },
    handleCurrentChange(pageNum) {
      this.params.pageNum = pageNum;
      this.fetchTableData();
    }
  }
}
</script>
