```yml
affinity: {}
checkInterval: 30
concurrent: 10
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
  node-role.kubernetes.io/worker: 'true'
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
    enabled: true
    resourceNames:
      - gitlab-runner
  rules: []
resources: {}
runners:
  cache:
    cacheType: File
    path: /cache
  config: |
    [[runners]]
      [runners.kubernetes]
        namespace = "{{.Release.Namespace}}"
        image = "ubuntu:16.04"
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
volumeMounts:
  - mountPath: /cache
    name: gitlab-runner-cache
volumes:
  - name: gitlab-runner-cache
    persistentVolumeClaim:
      claimName: gitlab-runner-0
certsSecretName: git.run.crt
gitlabUrl: https://git.run
global:
  cattle:
    systemProjectId: p-xlzwq
runnerToken: glrt-TShDfMyABYzto8Tm5BzK
```
