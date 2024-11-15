# WEEK 9 - CKA Book Course

Access the Book Here: [AcingTheCKA.com](https://acingthecka.com)

[WEEK 9 - Meeting Recording](https://community.kubeskills.com/c/meetings/cka-exercise-review-exam-preparation)

## Chapter 9 Overview
- The most important aspects of the exam
- Preparing for exam day
- Review of the Kubernetes documentation
- Accessing your free practice exam
- Accessing a free cheat sheet for kubectl commands

## CHAPTER 9 CHALLENGE

- [https://community.kubeskills.com/c/welcome-to-the-cka/exam-simulator-solutions](https://community.kubeskills.com/c/welcome-to-the-cka/exam-simulator-solutions)

## LINKS

- [Killercoda Exam Environment Simulator](https://killercoda.com/kimwuestkamp/scenario/cks-cka-ckad-remote-desktop)
- [Killer Shell - Exam Simulator](https://killer.sh)
- [Additional Killercoda Exercises - CKA](https://killercoda.com/cka)
- [Using PSI Bridge - LF Exam Handbook](https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2)

## FAQ

1. What is the format of the CKA exam?
The CKA exam is a practical, hands-on exam taken remotely. There are no multiple choice questions. Instead, you are presented with a series of tasks to perform in a live Kubernetes cluster environment. You will have access to a terminal and a web browser to access Kubernetes documentation and the Kubernetes GitHub page.

2. Where can I practice for the CKA exam?
The CKA Exam Simulator provided by Killer.sh is highly recommended. You can access it through your Linux Foundation training portal. The simulator provides a realistic exam environment with sample questions similar to the actual exam. It is also recommended to practice the exercises in the CKA course book using a local Kind cluster or the Killercoda environment, which offers a simulated exam environment with a remote desktop.

3. What is the passing score for the CKA exam?
You must achieve a score of 66% or higher to pass the CKA exam. Certain sections, such as troubleshooting, may carry a higher percentage of the overall score, so it's essential to focus on those areas during your preparation.

4. What are the requirements for my workspace during the exam?
You must take the exam in a quiet, private room with a closed door, free from distractions and outside noise. Your desk surface should be clear of any items that could be perceived as recording devices. External monitors should be unplugged or, ideally, removed from the room. You will be required to show your proctor the entire room using your webcam.

5. What resources can I access during the exam?
You are allowed to have a web browser open during the exam, but you can only access two websites: the official Kubernetes documentation (kubernetes.io/docs) and the Kubernetes GitHub page (github.com/kubernetes). It's important to be familiar with the documentation and use the search function effectively to save time.

6. What is the importance of using the "kubectl context" command during the exam?
The kubectl context command is used to manage multiple Kubernetes clusters. During the CKA exam, you will be given access to various clusters. The kubectl context command allows you to switch between these clusters and execute commands in the correct context. The exam simulator will provide the appropriate kubectl context commands for each task.

7. How do liveness and readiness probes work in Kubernetes?
Liveness probes check if a container is running properly. If a liveness probe fails, Kubernetes restarts the container.
Readiness probes determine if a container is ready to receive traffic. A container is only added to a service's endpoint list if its readiness probe passes.

8. How can I sort Kubernetes pods by their age?
You can use the kubectl get pods command with the `--sort-by=.metadata.creationTimestamp` flag to list pods sorted by their age (oldest to newest).