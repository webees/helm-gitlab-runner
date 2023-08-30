```yml
affinity:
  podAntiAffinity:
    preferredDuringSchedulingIgnoredDuringExecution:
      - podAffinityTerm:
          labelSelector:
            matchExpressions:
              - key: chart
                operator: In
                values:
                  - gitlab-runner-0.56.0
          topologyKey: kubernetes.io/hostname
        weight: 100
checkInterval: 30
concurrent: 3
configMaps: {}
hostAliases: []
image:
  image: gitlab-org/gitlab-runner
  registry: registry.gitlab.com
imagePullPolicy: IfNotPresent
metrics:
  enabled: false
  port: 9252
  portName: metrics
  serviceMonitor:
    enabled: false
nodeSelector:
  app.runner: ''
podAnnotations: {}
podLabels: {}
podSecurityContext:
  fsGroup: 65533
  runAsUser: 100
priorityClassName: ''
rbac:
  clusterWideAccess: false
  create: true
  podSecurityPolicy:
    enabled: false
    resourceNames:
      - gitlab-runner
  rules: []
resources: {}
runners:
  cache: {}
  config: |
    [[runners]]
      [runners.kubernetes]
        namespace = "{{.Release.Namespace}}"
        image = "ubuntu:22.04"
        [runners.kubernetes.node_selector]
          "app.runner" = ""
        [[runners.kubernetes.volumes.empty_dir]]
          name = "tmpfs"
          mount_path = "/builds"
          medium = "Memory"
        [[runners.kubernetes.volumes.secret]]
          name = "gitlab-runner-certs"
          mount_path = "/etc/gitlab-runner/certs/"
secrets: []
securityContext:
  allowPrivilegeEscalation: false
  capabilities:
    drop:
      - ALL
  privileged: false
  readOnlyRootFilesystem: false
  runAsNonRoot: true
service:
  enabled: false
  type: ClusterIP
sessionServer:
  enabled: false
terminationGracePeriodSeconds: 3600
tolerations: []
useTini: false
volumeMounts: []
volumes: []
certsSecretName: gitlab-runner-certs
gitlabUrl: https://git.run
global:
  cattle:
    systemProjectId: p-xlzwq
runnerToken: glrt-6YDmWgf-TZ9zjRsxqc-w

```
