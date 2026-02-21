### 系统介绍

基于SpringBoot和Vue实现的校园社团管理系统采用前后端分离的架构方式，系统共有三个角色：用户、社团管理员和系统管理员。用户实现了注册/登录、社团信息浏览、社团活动浏览、入团申请记录、社团费用记录等功能模块，社团管理员实现了社团信息浏览、社团成员管理、入团申请处理、社团活动浏览、通知信息管理、费用记录管理等功能模块，系统管理员实现了系统用户管理、社团类型管理、社团信息管理、社团成员管理、社团活动管理、通知信息管理、入团申请记录、费用记录管理等功能模块。

### 技术选型

开发工具：idea2020.3+Webstorm2020.3

运行环境：jdk1.8+maven3.6.0+MySQL5.7+nodejs14.21.3

服务端技术：Springboot+Mybatis-Plus+SpringSecurity+Fastjson

前端技术：html+css+Vue+axios+Element-UI+echarts

### 成果展示

用户->注册/登录
<img width="1901" height="1024" alt="登录注册" src="https://github.com/user-attachments/assets/6b63c414-557e-4d69-a89a-a6db859c0e74" />

用户->社团信息浏览
<img width="1917" height="1099" alt="用户-社团信息浏览" src="https://github.com/user-attachments/assets/d51fdc50-4571-406c-a937-818dacdd167f" />

用户->社团活动浏览
<img width="1920" height="1099" alt="用户-社团活动浏览" src="https://github.com/user-attachments/assets/a3ae1590-bd33-47f1-930a-fd5d6b46838f" />

用户->入团申请记录
<img width="1912" height="1097" alt="用户-入团申请记录" src="https://github.com/user-attachments/assets/68516861-2db4-4af9-a259-4d1a79e4ccf4" />

用户->社团费用记录
<img width="1920" height="1094" alt="用户-社团费用记录" src="https://github.com/user-attachments/assets/a00db587-1899-4396-ab6a-8d72a46f2634" />

社团管理员->社团成员管理
<img width="1916" height="1101" alt="社团管理员-社团成员管理" src="https://github.com/user-attachments/assets/8e078e14-3aba-41cb-831d-4d0f72cd3512" />

社团管理员->入团申请处理
<img width="1920" height="1097" alt="社团管理员-入团申请处理" src="https://github.com/user-attachments/assets/03b0ea42-5e40-4d7e-819e-743d83463014" />

社团管理员->通知信息管理
<img width="1920" height="1097" alt="社团管理员-通知信息管理" src="https://github.com/user-attachments/assets/bd06b3af-9167-4a59-9641-9d19b2d860f4" />

社团管理员->费用记录管理
<img width="1920" height="1097" alt="社团管理员-费用记录管理" src="https://github.com/user-attachments/assets/8f1ddeb9-eda9-41c4-83b4-2d411a2194fb" />

系统管理员->系统用户管理
<img width="1920" height="1097" alt="系统管理员-系统用户管理" src="https://github.com/user-attachments/assets/850353e9-84cf-4777-9efd-fd2c626e1d68" />

系统管理员->社团类型管理
<img width="1920" height="1095" alt="系统管理员-社团类型管理" src="https://github.com/user-attachments/assets/a21b1172-8d83-4518-a643-cb698338d2dd" />

系统管理员->社团信息管理
<img width="1920" height="1101" alt="系统管理员-社团信息管理" src="https://github.com/user-attachments/assets/3108126a-e205-4739-9ed1-65e8cb59fa76" />

系统管理员->社团成员管理
<img width="1920" height="1095" alt="系统管理员-社团成员管理" src="https://github.com/user-attachments/assets/e47a5dbc-a556-43a0-9420-6d83f6ad7472" />

系统管理员->社团活动管理
<img width="1920" height="1100" alt="系统管理员-社团活动管理" src="https://github.com/user-attachments/assets/f33fdd81-ce25-4ddd-a386-2e247ad3a9d2" />

### 源码展示

@Controller

@RequestMapping("/teamTypes")

public class TeamTypesController extends BaseController {

protected static final Logger Log = LoggerFactory.getLogger(TeamTypesController.class);

@Autowired

private TeamTypesService teamTypesService;

@GetMapping("/all")

@ResponseBody

public R getAll(){

    Log.info("查看全部的社团类型信息");

    List<TeamTypes> list = teamTypesService.getAll();

    return R.successData(list);
    
}

@GetMapping("/info")

@ResponseBody

public R getInfo(String id) {

    Log.info("查找指定社团类型，ID：{}", id);

    TeamTypes teamTypes = teamTypesService.getOne(id);

    return R.successData(teamTypes);
    
}

@GetMapping("/page")

@ResponseBody

public R getPageInfos(Long pageIndex, Long pageSize,
                      TeamTypes teamTypes) {

    Log.info("分页查找社团类型，当前页码：{}，"
                    + "每页数据量：{}, 模糊查询，附加参数：{}", pageIndex,
            pageSize, teamTypes);

    PageData page = teamTypesService.getPageInfo(pageIndex, pageSize, teamTypes);

    return R.successData(page);
    
}

@PostMapping("/add")

@ResponseBody

public R addInfo(TeamTypes teamTypes) {

    teamTypes.setId(IDUtils.makeIDByCurrent());
    teamTypes.setCreateTime(DateUtils.getNowDate());

    Log.info("添加社团类型，传入参数：{}", teamTypes);

    teamTypesService.add(teamTypes);

    return R.success();
    
}

@PostMapping("/upd")

@ResponseBody

public R updInfo(TeamTypes teamTypes) {

    Log.info("修改社团类型，传入参数：{}", teamTypes);

    teamTypesService.update(teamTypes);

    return R.success();
    
}

@PostMapping("/del")

@ResponseBody

public R delInfo(String id) {

    if(teamTypesService.isRemove(id)){

        Log.info("删除社团类型, ID:{}", id);

        TeamTypes teamTypes = teamTypesService.getOne(id);

        teamTypesService.delete(teamTypes);

        return R.success();
    }else{

        return R.warn("存在关联社团，无法移除");
    }
    
}

}

### 账号地址及其它说明

1、地址说明

登录页：localhost:8080

2、账号说明

用户：zhangsan/123456

社团管理员：zhazha/123456

系统管理员：admin/123456

3、目录结构展示

<img width="709" height="179" alt="目录结构展示" src="https://github.com/user-attachments/assets/4f97486a-57a3-4024-9586-da7906b7e5b1" />

4、项目结构展示

<img width="1717" height="945" alt="项目结构展示" src="https://github.com/user-attachments/assets/adc97051-83ab-4fa6-91b1-16ef7e346efc" />

5、运行步骤

1）创建数据库、导入sql脚本

2）修改application.yml中的数据库配置文件，启动服务端

3）在client目录下打开cmd，执行npm install或者yarn install下载依赖

4）下载完毕后启动前端npm run serve，访问端口

获取方式(可远程调试)
访问链接：https://mbd.pub/o/bread/mbd-aJeVlJlu

若资源获取失败，可添加happy35596339(vx)或2061772307(qq)进行交流
