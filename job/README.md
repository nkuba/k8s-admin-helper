# NAME

A job creates one or more pods and ensures that a specified number of them successfully terminate.

## Resources
* [Documentation](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/)
* [API Reference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.9/#job-v1-batch)

## Kubectl commands

`kubectl get xxx`

## Manifests

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: pi
spec:
  template:
    spec:
      containers:
      - name: pi
        image: perl
        command: ["perl",  "-Mbignum=bpi", "-wle", "print bpi(2000)"]
      restartPolicy: Never # Other possibility: OnFailure
  backoffLimit: 4
#  Parallel Jobs - Fixed Completion Count job
#  You can set "parallelism" if you want parallel execution of jobs
  completions: 5
#  Parallel Jobs - Work Queue Job job
#  Do not set "completions"
  parallelism: 2
```