# CC

## OpenTelemetry

官网：[opentelementry](https://opentelemetry.io)

自动埋点库： [github](https://github.com/open-telemetry/opentelemetry-java-instrumentation)

## k8s operator模式

[operator模式](https://kubernetes.io/zh/docs/concepts/extend-kubernetes/operator/)

## elasticsearch

`casecloud/addons/monitoring/elasticsearch/`，all-in-one.yaml是自定义资源和operator，elasticsearch.yaml是实质的定义,还有获得elasticsearch的密码的脚本。

参考文档：[elasticsearch](https://www.elastic.co/guide/en/cloud-on-k8s/current/k8s-deploy-elasticsearch.html)

## Jaeger

埋点后将数据发给agent，agent将数据发送给collector，collector将数据整理后存到elasticsearch中，query从elasticsearch中查询数据并向外展示。

Jaeger配置：`casecloud/addons/monitoring/jaeger/`

Jaeger参考网址：[Jaeger](https://www.jaegertracing.io/docs/1.23/operator/)

待配置：cleaner、rollover和dependencies

## Prometheus和grafana

使用了kube-prometheus的方式，crd和operator放在了`/manifests/setup/`文件夹中，其余组件的配置在`/manifests`中。

prometheus operator的抽象：[]()

