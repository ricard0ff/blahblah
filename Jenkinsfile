node {
  def keyFile = '/var/jenkins_home/creds.json'
  def project = 'jens-cluster-test'
  def appName = 'gg-web'
  sh("/var/jenkins_home/google-cloud-sdk/bin/gcloud auth activate-service-account --key-file=${keyFile} --project=${project}")
  sh("export GOOGLE_APPLICATION_CREDENTIALS=${keyFile}")
  sh("/var/jenkins_home/google-cloud-sdk/bin/gcloud container clusters get-credentials jens-cluster-test --zone=us-central1-a --project=${project}")
  sh("/var/jenkins_home/kubernetes/client/bin/kubectl get pods --all-namespaces")
  sh("/var/jenkins_home/kubernetes/client/bin/kubectl get namespaces")
  sh("/var/jenkins_home/kubernetes/client/bin/kubectl --namespace=default create secret docker-registry gcr-json-key-3 --docker-server=https://gcr.io --docker-username=_json_key --docker-email=blah@blah.com --docker-password=\"\$(cat /var/jenkins_home/gcr.json)\"")
  sh("/var/jenkins_home/kubernetes/client/bin/kubectl --namespace=default patch serviceaccount default -p '{\"imagePullSecrets\": [{\"name\": \"gcr-json-key-3\"}]}'")
  sh("/var/jenkins_home/kubernetes/client/bin/kubectl run test-app-4 --image=gcr.io/mgcp-ops-sandbox/blahblah:v1 --port 8080 --namespace=default")
}
