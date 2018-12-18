<template>
  <div class="app-container calendar-list-container">
    <div class="filter-container">
      <el-input @keyup.enter.native="handleFilter" style="width: 200px;" class="filter-item" placeholder="姓名或账户" v-model="listQuery.name"> </el-input>
      <el-button class="filter-item" type="primary" v-waves icon="search" @click="handleFilter">搜索</el-button>
      <el-button class="filter-item" v-if="baseMenuCopyManager_btn_add" style="margin-left: 10px;" @click="handleCreate" type="primary" icon="edit">添加</el-button>
    </div>
    <el-table :key='tableKey' :data="list" v-loading.body="listLoading" border fit highlight-current-row style="width: 100%">

      <el-table-column align="center" label="id" width="65">
      <template scope="scope">
        <span>{{scope.row.id}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="路径编码">
      <template scope="scope">
        <span>{{scope.row.code}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="标题">
      <template scope="scope">
        <span>{{scope.row.title}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="父级节点">
      <template scope="scope">
        <span>{{scope.row.parentId}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="资源路径">
      <template scope="scope">
        <span>{{scope.row.href}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="图标">
      <template scope="scope">
        <span>{{scope.row.icon}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.type}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="排序">
      <template scope="scope">
        <span>{{scope.row.orderNum}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="描述">
      <template scope="scope">
        <span>{{scope.row.description}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="菜单上下级关系">
      <template scope="scope">
        <span>{{scope.row.path}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="启用禁用">
      <template scope="scope">
        <span>{{scope.row.enabled}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.crtTime}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.crtUser}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.crtName}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.crtHost}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.updTime}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.updUser}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.updName}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.updHost}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.attr1}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.attr2}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.attr3}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.attr4}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.attr5}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.attr6}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.attr7}}</span>
      </template>
    </el-table-column>
        <el-table-column width="200px" align="center" label="">
      <template scope="scope">
        <span>{{scope.row.attr8}}</span>
      </template>
    </el-table-column>
        <el-table-column fixed="right" align="center" label="操作" width="150"> <template scope="scope">
        <el-button v-if="baseMenuCopyManager_btn_edit" size="small" type="success" @click="handleUpdate(scope.row)">编辑
        </el-button>
        <el-button v-if="baseMenuCopyManager_btn_del" size="small" type="danger" @click="handleDelete(scope.row)">删除
        </el-button>
      </template> </el-table-column>
    </el-table>
    <div v-show="!listLoading" class="pagination-container">
      <el-pagination @size-change="handleSizeChange" @current-change="handleCurrentChange" :current-page.sync="listQuery.page" :page-sizes="[10,20,30, 50]" :page-size="listQuery.limit" layout="total, sizes, prev, pager, next, jumper" :total="total"> </el-pagination>
    </div>
    <el-dialog :title="textMap[dialogStatus]" :visible.sync="dialogFormVisible">
      <el-form :model="form" :rules="rules" ref="form" label-width="100px">
        <el-form-item label="路径编码" prop="code">
      <el-input v-model="form.code" placeholder="请输入路径编码"></el-input>
    </el-form-item>
        <el-form-item label="标题" prop="title">
      <el-input v-model="form.title" placeholder="请输入标题"></el-input>
    </el-form-item>
        <el-form-item label="父级节点" prop="parentId">
      <el-input v-model="form.parentId" placeholder="请输入父级节点"></el-input>
    </el-form-item>
        <el-form-item label="资源路径" prop="href">
      <el-input v-model="form.href" placeholder="请输入资源路径"></el-input>
    </el-form-item>
        <el-form-item label="图标" prop="icon">
      <el-input v-model="form.icon" placeholder="请输入图标"></el-input>
    </el-form-item>
        <el-form-item label="" prop="type">
      <el-input v-model="form.type" placeholder="请输入"></el-input>
    </el-form-item>
        <el-form-item label="排序" prop="orderNum">
      <el-input v-model="form.orderNum" placeholder="请输入排序"></el-input>
    </el-form-item>
        <el-form-item label="描述" prop="description">
      <el-input v-model="form.description" placeholder="请输入描述"></el-input>
    </el-form-item>
        <el-form-item label="菜单上下级关系" prop="path">
      <el-input v-model="form.path" placeholder="请输入菜单上下级关系"></el-input>
    </el-form-item>
        <el-form-item label="启用禁用" prop="enabled">
      <el-input v-model="form.enabled" placeholder="请输入启用禁用"></el-input>
    </el-form-item>
        <el-form-item label="" prop="crtTime">
      <el-input v-model="form.crtTime" placeholder="请输入"></el-input>
    </el-form-item>
        <el-form-item label="" prop="crtUser">
      <el-input v-model="form.crtUser" placeholder="请输入"></el-input>
    </el-form-item>
        <el-form-item label="" prop="crtName">
      <el-input v-model="form.crtName" placeholder="请输入"></el-input>
    </el-form-item>
        <el-form-item label="" prop="crtHost">
      <el-input v-model="form.crtHost" placeholder="请输入"></el-input>
    </el-form-item>
        <el-form-item label="" prop="updTime">
      <el-input v-model="form.updTime" placeholder="请输入"></el-input>
    </el-form-item>
        <el-form-item label="" prop="updUser">
      <el-input v-model="form.updUser" placeholder="请输入"></el-input>
    </el-form-item>
        <el-form-item label="" prop="updName">
      <el-input v-model="form.updName" placeholder="请输入"></el-input>
    </el-form-item>
        <el-form-item label="" prop="updHost">
      <el-input v-model="form.updHost" placeholder="请输入"></el-input>
    </el-form-item>
        <el-form-item label="" prop="attr1">
      <el-input v-model="form.attr1" placeholder="请输入"></el-input>
    </el-form-item>
        <el-form-item label="" prop="attr2">
      <el-input v-model="form.attr2" placeholder="请输入"></el-input>
    </el-form-item>
        <el-form-item label="" prop="attr3">
      <el-input v-model="form.attr3" placeholder="请输入"></el-input>
    </el-form-item>
        <el-form-item label="" prop="attr4">
      <el-input v-model="form.attr4" placeholder="请输入"></el-input>
    </el-form-item>
        <el-form-item label="" prop="attr5">
      <el-input v-model="form.attr5" placeholder="请输入"></el-input>
    </el-form-item>
        <el-form-item label="" prop="attr6">
      <el-input v-model="form.attr6" placeholder="请输入"></el-input>
    </el-form-item>
        <el-form-item label="" prop="attr7">
      <el-input v-model="form.attr7" placeholder="请输入"></el-input>
    </el-form-item>
        <el-form-item label="" prop="attr8">
      <el-input v-model="form.attr8" placeholder="请输入"></el-input>
    </el-form-item>
        </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="cancel('form')">取 消</el-button>
        <el-button v-if="dialogStatus=='create'" type="primary" @click="create('form')">确 定</el-button>
        <el-button v-else type="primary" @click="update('form')">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
  import {
      page,
      addObj,
      getObj,
      delObj,
      putObj
  } from 'api/auth/baseMenuCopy/index';
  import { mapGetters } from 'vuex';
  export default {
    name: 'baseMenuCopy',
    data() {
      return {
        form: {
          code: undefined,
          title: undefined,
          parentId: undefined,
          href: undefined,
          icon: undefined,
          type: undefined,
          orderNum: undefined,
          description: undefined,
          path: undefined,
          enabled: undefined,
          crtTime: undefined,
          crtUser: undefined,
          crtName: undefined,
          crtHost: undefined,
          updTime: undefined,
          updUser: undefined,
          updName: undefined,
          updHost: undefined,
          attr1: undefined,
          attr2: undefined,
          attr3: undefined,
          attr4: undefined,
          attr5: undefined,
          attr6: undefined,
          attr7: undefined,
          attr8: undefined
        },
        rules: {
          code: [
            {
              required: true,
              message: '请输入路径编码',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          title: [
            {
              required: true,
              message: '请输入标题',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          parentId: [
            {
              required: true,
              message: '请输入父级节点',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          href: [
            {
              required: true,
              message: '请输入资源路径',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          icon: [
            {
              required: true,
              message: '请输入图标',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          type: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          orderNum: [
            {
              required: true,
              message: '请输入排序',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          description: [
            {
              required: true,
              message: '请输入描述',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          path: [
            {
              required: true,
              message: '请输入菜单上下级关系',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          enabled: [
            {
              required: true,
              message: '请输入启用禁用',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          crtTime: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          crtUser: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          crtName: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          crtHost: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          updTime: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          updUser: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          updName: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          updHost: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          attr1: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          attr2: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          attr3: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          attr4: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          attr5: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          attr6: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          attr7: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ],
          attr8: [
            {
              required: true,
              message: '请输入',
              trigger: 'blur'
            },
            {
              min: 3,
              max: 20,
              message: '长度在 3 到 20 个字符',
              trigger: 'blur'
            }
          ]
        },
        list: null,
        total: null,
        listLoading: true,
        listQuery: {
          page: 1,
          limit: 20,
          name: undefined
        },
        dialogFormVisible: false,
        dialogStatus: '',
        baseMenuCopyManager_btn_edit: false,
        baseMenuCopyManager_btn_del: false,
        baseMenuCopyManager_btn_add: false,
        textMap: {
          update: '编辑',
          create: '创建'
        },
        tableKey: 0
      }
    },
    created() {
      this.getList();
      this.baseMenuCopyManager_btn_edit = this.elements['baseMenuCopyManager:btn_edit'];
      this.baseMenuCopyManager_btn_del = this.elements['baseMenuCopyManager:btn_del'];
      this.baseMenuCopyManager_btn_add = this.elements['baseMenuCopyManager:btn_add'];
    },
    computed: {
      ...mapGetters([
        'elements'
      ])
    },
    methods: {
      getList() {
        this.listLoading = true;
        page(this.listQuery)
            .then(response => {
              this.list = response.data.rows;
              this.total = response.data.total;
              this.listLoading = false;
            })
      },
      handleFilter() {
        this.getList();
      },
      handleSizeChange(val) {
        this.listQuery.limit = val;
        this.getList();
      },
      handleCurrentChange(val) {
        this.listQuery.page = val;
        this.getList();
      },
      handleCreate() {
        this.resetTemp();
        this.dialogStatus = 'create';
        this.dialogFormVisible = true;
      },
      handleUpdate(row) {
        getObj(row.id)
            .then(response => {
              this.form = response.data;
              this.dialogFormVisible = true;
              this.dialogStatus = 'update';
            });
      },
      handleDelete(row) {
        this.$confirm('此操作将永久删除, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        })
            .then(() => {
              delObj(row.id)
            .then(() => {
              this.$notify({
                title: '成功',
                message: '删除成功',
                type: 'success',
                duration: 2000
              });
              const index = this.list.indexOf(row);
              this.list.splice(index, 1);
            })
            });
      },
      create(formName) {
        const set = this.$refs;
        set[formName].validate(valid => {
          if (valid) {
            addObj(this.form)
          .then(() => {
            this.dialogFormVisible = false;
            this.getList();
            this.$notify({
              title: '成功',
              message: '创建成功',
              type: 'success',
              duration: 2000
            });
          })
          } else {
            return false;
          }
        });
      },
      cancel(formName) {
        this.dialogFormVisible = false;
        const set = this.$refs;
        set[formName].resetFields();
      },
      update(formName) {
        const set = this.$refs;
        set[formName].validate(valid => {
          if (valid) {
            this.dialogFormVisible = false;
            this.form.password = undefined;
            putObj(this.form.id, this.form).then(() => {
              this.dialogFormVisible = false;
              this.getList();
              this.$notify({
                title: '成功',
                message: '创建成功',
                type: 'success',
                duration: 2000
              });
            });
          } else {
            return false;
          }
        });
      },
      resetTemp() {
        this.form = {
          username: undefined,
          name: undefined,
          sex: '男',
          password: undefined,
          description: undefined
        };
      }
    }
  }
</script>
