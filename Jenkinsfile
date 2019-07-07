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
        # Define the environment variable
        - name: DOCKERHUBUSER
          valueFrom:
            configMapKeyRef:
              # The ConfigMap containing the value you want to assign to SPECIAL_LEVEL_KEY
              name: dockerhub
              # Specify the key associated with the value
              key: user.name
        - name: DOCKERHUBPASS
          valueFrom:
            configMapKeyRef:
              # The ConfigMap containing the value you want to assign to SPECIAL_LEVEL_KEY
              name: dockerhub
              # Specify the key associated with the value
              key: user.pass
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
