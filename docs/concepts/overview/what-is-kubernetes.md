---
reviewers:
- bgrant0607
- mikedanese
title: What is Kubernetes?
title: Kubernetes란 무엇인가?
---

{% capture overview %}
This page is an overview of Kubernetes.
이 페이지는 Kubernetes의 개요입니다.
{% endcapture %}

{% capture body %}
Kubernetes is a portable, extensible open-source platform for managing
containerized workloads and services, that facilitates both
declarative configuration and automation. It has a large, rapidly
growing ecosystem. Kubernetes services, support, and tools are widely available.
Kubernetes는 간편하고, 컨테이너로된 작업들과 서비스를 관리하기 위한 확장 가능한 오픈소스 플랫폼입니다.
이것들은 설정과 자동화 모두를 쉽게 만들어 줍니다. 또한 크고 신속하게 성장하는 에코시스템을 가지고 있습니다.
Kubernetes의 서비스, 지원 그리고 도구들이 폭넓게 제공됩니다.


Google open-sourced the Kubernetes project in 2014. Kubernetes builds upon
a [decade and a half of experience that Google has with running
production workloads at
scale](https://research.google.com/pubs/pub43438.html), combined with
best-of-breed ideas and practices from the community.
구글은 2014년에 Kubernetes 프로젝트를 오픈소스화 했습니다.
Kubernetes는 구글의 대규모 운영 환경에서 십년 반의 경험 위에서 발전되어 왔습니다.
더불어 커뮤니티로 부터 최고의 아이디어와 사례들이 결합되어졌습니다.


#### Why do I need Kubernetes and what can it do?
#### 왜 나는 Kubernetes가 필요하고, Kubernetes는 무엇을 해줄 수 있을까?

Kubernetes has a number of features. It can be thought of as:
* a container platform
* a microservices platform
* a portable cloud platform
and a lot more.
Kubernetes에는 많은 기능들이 있습니다. 아래와 같은 것들을 생각할 수 있을 것입니다.:
* 컨테이너 플래폼
* 마이크로서비스 플랫폼
* 포터블한 클라우드 플랫폼 등


Kubernetes provides a **container-centric** management environment. It
orchestrates computing, networking, and storage infrastructure on
behalf of user workloads. This provides much of the simplicity of
Platform as a Service (PaaS) with the flexibility of Infrastructure as
a Service (IaaS), and enables portability across infrastructure
providers.
Kubernetes는 컨테이너 중심의 관리 환경을 제공합니다.
사용자의 워크로드를 대신하여 컴퓨팅, 네트워크, 저장소 인프라 환경을 조정합니다.
이것들은 IaaS의 유연함을 갖추면서 PaaS의 매우 단순함을 제공합니다.
그리고 인프라 제공업체 간의 이동을 가능하게 합니다.


#### How is Kubernetes a platform?
#### Kubernetes는 어떻게 플랫폼이 되는가?

Even though Kubernetes provides a lot of functionality, there are
always new scenarios that would benefit from new
features. Application-specific workflows can be streamlined to
accelerate developer velocity. Ad hoc orchestration that is acceptable
initially often requires robust automation at scale. This is why
Kubernetes was also designed to serve as a platform for building an
ecosystem of components and tools to make it easier to deploy, scale,
and manage applications.

[Labels](/docs/concepts/overview/working-with-objects/labels/) empower
users to organize their resources however they
please. [Annotations](/docs/concepts/overview/working-with-objects/annotations/)
enable users to decorate resources with custom information to
facilitate their workflows and provide an easy way for management
tools to checkpoint state.

Additionally, the [Kubernetes control
plane](/docs/concepts/overview/components/) is built upon the same
[APIs](/docs/reference/api-overview/) that are available to developers
and users. Users can write their own controllers, such as
[schedulers](https://github.com/kubernetes/community/blob/{{page.githubbranch}}/contributors/devel/scheduler.md),
with [their own
APIs](/docs/concepts/api-extension/custom-resources/)
that can be targeted by a general-purpose [command-line
tool](/docs/user-guide/kubectl-overview/).

This
[design](https://git.k8s.io/community/contributors/design-proposals/architecture/architecture.md)
has enabled a number of other systems to build atop Kubernetes.

#### What Kubernetes is not

Kubernetes is not a traditional, all-inclusive PaaS (Platform as a
Service) system. Since Kubernetes operates at the container level
rather than at the hardware level, it provides some generally
applicable features common to PaaS offerings, such as deployment,
scaling, load balancing, logging, and monitoring. However, Kubernetes
is not monolithic, and these default solutions are optional and
pluggable. Kubernetes provides the building blocks for building developer
platforms, but preserves user choice and flexibility where it is
important.

Kubernetes:

* Does not limit the types of applications supported. Kubernetes aims
  to support an extremely diverse variety of workloads, including
  stateless, stateful, and data-processing workloads. If an
  application can run in a container, it should run great on
  Kubernetes.
* Does not deploy source code and does not build your
  application. Continuous Integration, Delivery, and Deployment
  (CI/CD) workflows are determined by organization cultures and preferences
  as well as technical requirements.
* Does not provide application-level services, such as middleware
  (e.g., message buses), data-processing frameworks (for example,
  Spark), databases (e.g., mysql), caches, nor cluster storage systems (e.g.,
  Ceph) as built-in services. Such components can run on Kubernetes, and/or
  can be accessed by applications running on Kubernetes through portable
  mechanisms, such as the Open Service Broker.
* Does not dictate logging, monitoring, or alerting solutions. It provides
  some integrations as proof of concept, and mechanisms to collect and
  export metrics.
* Does not provide nor mandate a configuration language/system (e.g.,
  [jsonnet](https://github.com/google/jsonnet)). It provides a declarative
  API that may be targeted by arbitrary forms of declarative specifications.
* Does not provide nor adopt any comprehensive machine configuration,
  maintenance, management, or self-healing systems.

Additionally, Kubernetes is not a mere *orchestration system*. In
fact, it eliminates the need for orchestration. The technical
definition of *orchestration* is execution of a defined workflow:
first do A, then B, then C. In contrast, Kubernetes is comprised of a
set of independent, composable control processes that continuously
drive the current state towards the provided desired state. It
shouldn't matter how you get from A to C. Centralized control is also
not required. This results in a system that is easier to use and more
powerful, robust, resilient, and extensible.

#### Why containers?

Looking for reasons why you should be using containers?

![Why Containers?](/images/docs/why_containers.svg)

The *Old Way* to deploy applications was to install the applications
on a host using the operating-system package manager. This had the
disadvantage of entangling the applications' executables,
configuration, libraries, and lifecycles with each other and with the
host OS. One could build immutable virtual-machine images in order to
achieve predictable rollouts and rollbacks, but VMs are heavyweight
and non-portable.

The *New Way* is to deploy containers based on operating-system-level
virtualization rather than hardware virtualization. These containers
are isolated from each other and from the host: they have their own
filesystems, they can't see each others' processes, and their
computational resource usage can be bounded. They are easier to build
than VMs, and because they are decoupled from the underlying
infrastructure and from the host filesystem, they are portable across
clouds and OS distributions.

Because containers are small and fast, one application can be packed
in each container image. This one-to-one application-to-image
relationship unlocks the full benefits of containers. With containers,
immutable container images can be created at build/release time rather
than deployment time, since each application doesn't need to be
composed with the rest of the application stack, nor married to the
production infrastructure environment. Generating container images at
build/release time enables a consistent environment to be carried from
development into production.  Similarly, containers are vastly more
transparent than VMs, which facilitates monitoring and
management. This is especially true when the containers' process
lifecycles are managed by the infrastructure rather than hidden by a
process supervisor inside the container. Finally, with a single
application per container, managing the containers becomes tantamount
to managing deployment of the application.

Summary of container benefits:

* **Agile application creation and deployment**:
    Increased ease and efficiency of container image creation compared to VM image use.
* **Continuous development, integration, and deployment**:
    Provides for reliable and frequent container image build and
    deployment with quick and easy rollbacks (due to image
    immutability).
* **Dev and Ops separation of concerns**:
    Create application container images at build/release time rather
    than deployment time, thereby decoupling applications from
    infrastructure.
* **Observability**
    Not only surfaces OS-level information and metrics, but also application
    health and other signals.
* **Environmental consistency across development, testing, and production**:
    Runs the same on a laptop as it does in the cloud.
* **Cloud and OS distribution portability**:
    Runs on Ubuntu, RHEL, CoreOS, on-prem, Google Kubernetes Engine, and anywhere else.
* **Application-centric management**:
    Raises the level of abstraction from running an OS on virtual
    hardware to run an application on an OS using logical resources.
* **Loosely coupled, distributed, elastic, liberated [micro-services](https://martinfowler.com/articles/microservices.html)**:
    Applications are broken into smaller, independent pieces and can
    be deployed and managed dynamically -- not a fat monolithic stack
    running on one big single-purpose machine.
* **Resource isolation**:
    Predictable application performance.
* **Resource utilization**:
    High efficiency and density.

#### What does *Kubernetes* mean? K8s?

The name **Kubernetes** originates from Greek, meaning *helmsman* or
*pilot*, and is the root of *governor* and
[cybernetic](http://www.etymonline.com/index.php?term=cybernetics). *K8s*
is an abbreviation derived by replacing the 8 letters "ubernete" with
"8".

{% endcapture %}

{% capture whatsnext %}
*   Ready to [Get Started](/docs/setup/)?
*   For more details, see the [Kubernetes Documentation](/docs/home/).
{% endcapture %}
{% include templates/concept.md %}

