## 说明

利用Kustomize+Git方式组织管理各环境各服务k8s yaml配置。

- Kustomize是一种k8s原生的yaml配置文件管理方式；
- 通过Base&Overlays方式维护不同环境、不同集群的应用配置，实现配置复用；
- 利用Git Repo托管，可充分发挥git 版本控制、多人协作、集中管理、修改记录审计等优势。
- 线上线下配置同步一致，具备一定存档备份效果；
- 结合gitops cd可快速复制扩展多环境，多集群；


## 目录结构
```sh
├── apps                             # 所有业务服务配置文件目录
│   ├── base                         # 各服务不通环境基础配置文件（通用性配置）
│   │   ├── service-demo-1
│   │   ├── service-demo-2
│   │   ├── service-demo-3
│   └── qa                           # 对应环境各服务配置信息（可根据namespace划分）
│   │   ├── service-demo-1
│   │   ├── service-demo-2
│   │   ├── service-demo-3
│   └── staging
│       ├── service-demo-1
│       ├── service-demo-2
│       └── service-demo-3
├── clusters                        # 各集群主入口目录（可根据具体k8s集群划分）
│   ├── k8s-cluster-1
│   └── ├── apps-ns-test.yaml       # k8s-cluster-1集群中test环境apps索引入口文件；
│       ├── apps-ns-staging.yaml
│       ├── images-update-policy    # apps服务镜像自动更新策略目录；
│       └── infrastructure.yaml     # k8s-cluster-1集群基础中间件服务索引入口文件；
├── infrastructure                  # 各集群基础组建类服务
    ├── base                        # 基础组建基础配置
    │   ├── node-local-dns
    │   └── traefik-v2
    └── k8s-cluster-1              # 基础组建针对不同集群差异化配置
        ├── kustomization.yaml
        ├── node-local-dns
        └── traefik-v2
```
