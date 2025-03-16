# QuizApp Helm Charts

This repository contains Helm charts for deploying the QuizApp. The charts are hosted on GitHub Pages at [quizapp-charts.jotamario.lat](https://quizapp-charts.jotamario.lat).

## Prerequisites

- Kubernetes 1.12+
- Helm 3.0+

## Installing the Charts

To install the chart with the release name `my-release`:
```bash
helm repo add quizapp https://quizapp-charts.jotamario.lat
helm repo update
helm install my-release quizapp/quizapp-backend
helm install my-release quizapp/quizapp-frontend
helm install my-release quizapp/quizapp-ingress
```

## Uninstalling the Charts

To uninstall/delete the `my-release` deployment:
```bash
helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the QuizApp charts and their default values.

| Parameter                | Description                           | Default                        |
|--------------------------|---------------------------------------|--------------------------------|
| `replicaCount`           | Number of replicas                    | `1`                            |
| `image.repository`       | Image repository                      | `juanparraiv/quizapp-backend`  |
| `image.tag`              | Image tag                             | `1.0.0`                        |
| `image.pullPolicy`       | Image pull policy                     | `Always`                       |
| `service.type`           | Kubernetes service type               | `ClusterIP`                    |
| `service.port`           | Service port                          | `80`                           |
| `service.targetPort`     | Target port                           | `5000`                         |
| `ingress.enabled`        | Enable ingress                        | `false`                        |
| `ingress.hosts`          | Ingress hosts                         | `chart-example.local`          |
| `resources`              | Resource requests and limits          | `{}`                           |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example:
```bash
helm install my-release quizapp/quizapp-backend --set image.tag=2.0.0
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example:
```bash
helm install my-release quizapp/quizapp-backend -f values.yaml
```

## Accessing the Application

Once the chart is deployed, you can access the application using the following command:
```bash
kubectl port-forward svc/my-release-quizapp-backend 8080:80
```

Visit http://127.0.0.1:8080 to use your application.

## Testing the Deployment

To test the deployment, you can use the following command:
```bash
helm test my-release
```

This will run the test defined in the `templates/tests/test-connection.yaml`.

## Cleanup

To delete the deployment, use the following command:
```bash
helm delete my-release
```

This will remove all the Kubernetes components associated with the chart and delete the release.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.