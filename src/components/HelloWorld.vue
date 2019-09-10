<template>
  <el-container>
    <el-header>
      <el-button type="primary" @click="dialogFormVisible = true">添加</el-button>
    </el-header>
    <el-table
      :data="tableData"
      style="width: 100%">
      <el-table-column
        label="日期"
        width="180">
        <template slot-scope="scope">
          <i class="el-icon-time"></i>
          <span style="margin-left: 10px">{{ scope.row.date }}</span>
        </template>
      </el-table-column>
      <el-table-column
        label="姓名"
        width="180">
        <template slot-scope="scope">
          <el-popover trigger="hover" placement="top">
            <p>姓名: {{ scope.row.name }}</p>
            <p>住址: {{ scope.row.address }}</p>
            <div slot="reference" class="name-wrapper">
              <el-tag size="medium">{{ scope.row.name }}</el-tag>
            </div>
          </el-popover>
        </template>
      </el-table-column>
      <el-table-column
        label="性别"
        width="180">
        <template slot-scope="scope">
          <i class="el-icon-apple"></i>
          <span style="margin-left: 10px">{{ scope.row.sex }}</span>
        </template>
      </el-table-column>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button
            size="mini"
            @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
          <el-button
            size="mini"
            type="danger"
            @click="handleDelete(scope.$index, scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>


    <el-dialog title="添加用户" :visible.sync="dialogFormVisible">
      <el-form :model="user">
        <el-form-item label="日期" :label-width="formLabelWidth">
          <el-input v-model="user.date" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="姓名" :label-width="formLabelWidth">
          <el-input v-model="user.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="性别" :label-width="formLabelWidth">
          <el-input v-model="user.sex" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="地址" :label-width="formLabelWidth">
          <el-input v-model="user.address" autocomplete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="handleAdd()">确 定</el-button>
      </div>
    </el-dialog>


    <el-dialog title="更新用户" :visible.sync="updateDialogFormVisible">
      <el-form :model="user">
        <el-form-item label="日期" :label-width="formLabelWidth">
          <el-input v-model="user.date" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="姓名" :label-width="formLabelWidth">
          <el-input v-model="user.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="性别" :label-width="formLabelWidth">
          <el-input v-model="user.sex" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="地址" :label-width="formLabelWidth">
          <el-input v-model="user.address" autocomplete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="updateDialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="handleUpdate()">确 定</el-button>
      </div>
    </el-dialog>

  </el-container>
</template>

<script>
  export default {
    data() {
      return {
        formLabelWidth: '120px',
        dialogFormVisible: false,
        updateDialogFormVisible:false,
        user: {
          date: '',
          name: '',
          sex: '',
          address: ''
        },
        tableData: [{
          date: '2019-09-06',
          name: '李虎',
          sex: '男',
          address: '西安普陀区金沙江路 1508 弄'
        }, {
          date: '2019-09-07',
          name: '科龙',
          sex: '男',
          address: '北京市普陀区金沙江路 1517 弄'
        }, {
          date: '2019-09-08',
          name: '刘含',
          sex: '女',
          address: '上海市普陀区金沙江路 1519 弄'
        }, {
          date: '2019-09-09',
          name: '王小虎',
          sex: '男',
          address: '上海市普陀区金沙江路 1516 弄'
        }]
      }
    },
    methods: {
      handleAdd(){
        var _this = this;
        this.$message({
          type: 'success',
          message: '添加成功!'
        });
        _this.dialogFormVisible = false;
        this.tableData.push(this.user);
      },
      handleEdit(index, row) {
        this.user = row;
        this.updateDialogFormVisible = true;
      },
      handleUpdate(index, row) {
        console.log(index, row);
        var _this = this;
        this.$message({
          type: 'success',
          message: '更新成功!'
        });
        _this.updateDialogFormVisible = false;
      },
      handleDelete(index, row) {
        console.log(index, row);
        var _this = this;
        this.$confirm('此操作将永久删除该用户, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(
          () =>{
            _this.tableData.splice(_this.tableData.indexOf(row),1)
            this.$message({
              type: 'success',
              message: '删除成功!'
            });
          }
        );
      }
    }
  }
</script>
