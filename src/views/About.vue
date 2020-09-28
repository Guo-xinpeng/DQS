<template>
  <div class="about">
    <!-- 搜索框 -->
    <header>
      <el-input
        v-model="search"
        size="mini"
        placeholder="输入关键字搜索"
        clearable
        style="height:40px;width:200px"
      />
    </header>

    <el-table
      :data="list.filter(data => !search || data.username.toLowerCase().includes(search.toLowerCase()))
    "
      border
      style="width: 100%"
    >
      <el-table-column type="index"></el-table-column>
      <el-table-column label="姓名" prop="username"></el-table-column>
      <el-table-column prop="email" label="邮箱"></el-table-column>
      <el-table-column property="mobile" label="电话"></el-table-column>
      <el-table-column property="role_name" label="角色"></el-table-column>
      <el-table-column label="状态">
        <template slot-scope="scope">
          <el-switch
            v-model="scope.row.mg_state"
            active-color="#13ce66"
            inactive-color="#ff4949"
            @change="change(scope.row.mg_state,scope.row.id)"
          ></el-switch>
        </template>
      </el-table-column>
      <el-table-column prop="address" label="操作">
        <el-button type="primary" icon="el-icon-edit" circle></el-button>
        <el-button type="warning" icon="el-icon-star-off" circle></el-button>
        <!-- <el-button type="danger" icon="el-icon-delete" circle></el-button> -->
      </el-table-column>
    </el-table>
    <el-pagination
      @current-change="currentchange"
      @size-change="handleSizeChange"
      :current-page="1"
      :page-sizes="[2, 4,]"
      :page-size="100"
      layout="total, sizes, prev, pager, next, jumper"
      :total="length"
    ></el-pagination>
  </div>
</template>

  </div>
</template>


<script>
export default {
  data() {
    return {
      list: [],
      search: "",
      length: 0,
    };
  },
  mounted() {
    this.$axios({
      method: "get",
      url: `https://www.liulongbin.top:8888/api/private/v1/users`,
      headers: {
        Authorization: localStorage.getItem("TOKEN"),
      },
      params: {
        pagesize: 2,
        pagenum: 1,
      },
    }).then((res) => {
      this.list = res.data.data.users;
      this.length = res.data.data.total;
      console.log(res);
    });
  },
  beforeRouteEnter(to, from, next) {
    let token = localStorage.getItem("TOKEN") === null;

    // console.log(token);

    if (token) {
      next({ path: "/" });
    } else {
      next();
    }
  },

  methods: {
    handleSizeChange(val) {
      this.$axios({
        method: "get",
        url: `https://www.liulongbin.top:8888/api/private/v1/users`,
        headers: {
          Authorization: localStorage.getItem("TOKEN"),
        },
        params: {
          pagesize: val,
          pagenum: 1,
        },
      }).then((res) => {
        this.list = res.data.data.users;
        console.log(res);
      });
    },
    // 分页器
    currentchange(page) {
      // console.log(page)
      console.log(page);
      this.$axios({
        method: "get",
        url: `https://www.liulongbin.top:8888/api/private/v1/users`,
        headers: {
          Authorization: localStorage.getItem("TOKEN"),
        },
        params: {
          pagesize: 2,
          pagenum: page,
        },
      }).then((res) => {
        this.list = res.data.data.users;
        console.log(res);
      });
    },
  },
};
</script>

<style scoped>
header {
  width: 80%;
  display: flex;
  justify-content: space-between;
}
</style>
