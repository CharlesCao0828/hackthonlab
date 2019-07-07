def label = "docker-${UUID.randomUUID().toString()}"

podTemplate(label: label, yaml: """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: docker
    image: docker:1.11
    command: ['cat']
    env:
      -name: DOCKERHUBUSER
      valueFrom:
        configMapKeyRef:
          name: mydockerhub
          key: registry-login.username
      -name: DOCKERHUBPASS
        configMapKeyRef:
          name: mydockerhub
          key: registry-login.password
    tty: true
    volumeMounts:
    - name: dockersock
      mountPath: /var/run/docker.sock
  volumes:
  - name: dockersock
    hostPath:
      path: /var/run/docker.sock
  
"""
  ) {

  def image = "jenkins/jnlp-slave"
  node(label) {
    stage('Build Docker image') {
      container('docker') {
        sh "docker pull python"
        sh "docker tag python caozz0828/monster:v3"
        sh "env"
      }
    }
  }
}
