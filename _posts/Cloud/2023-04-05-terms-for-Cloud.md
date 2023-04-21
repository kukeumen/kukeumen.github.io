---
title: "클라우드 용어정리"
excerpt: "클라우드 관련 용어 정리"

categories:
  - Cloud
tags:
  - [Cloud, Docker, Terms]

permalink: /Cloud/Terms-for-Cloud/

toc: true
toc_sticky: true

date: 2023-04-05
last_modified_at: 2023-04-05
---

## 클라우드 관련 용어
*본 글은 완벽한 IT인프라 구축을 위찬 Docker (2판) 을 참고하여 작성되었습니다*

**온프레미스(on-premises)**: 자사에서 데이터센터를 보유하고 시스템 구축부터 운용까지를 모두 수행하는 형태의 시스템
- 초기 시스템 투자에 드는 비용 부담이 크며, 시스템 가동 후의 운용에 드는 비용도 시스템 이용량과 상관없이 일정 금액을 부담해야 함.

**퍼블릭 클라우드(public cloud)**: 인터넷을 통해 불특정 다수에게 제공되는 클라우드 서비스.
- 초기 투자 비용이 들지 않음.
- 제공할 서비스에 따라 IaaS/PaaS/SaaS/ 등이 있음.
  - IaaS(Infastructure-as-a-Service): 서비스로서의 인프라. 스토리지와 가상화 같은 인프라 서비스를 인터넷을 통해 클라우드로 제공함. AWS, Microsoft Azure, Google Cloud와 같은 퍼블릭 클라우드 공급업체가 IaaS의 예시임.
  - PaaS(Platforms-as-a-Service): 서비스로서의 플랫폼. 제공업체가 자체 인프라에서 하드웨어와 소프트웨어를 호스팅하고 이러한 플랫폼을 사용자에게 통합 솔루션, 솔루션 스택 또는 인터넷을 통한 서비스로 제공함. AWS Elastic Beanstalk, Heroku 및 Red Hat OpenShift 가 있음.
  - SaaS(Software-as-a-Service): 서비스로서의 소프트웨어. 가장 포괄적인 형식의 클라우드 컴퓨팅 서비스. 모든 애플리케이션은 제공업체가 관리하며 웹 브라우저를 통해 제공됨. Dropbox, Salesforce, Google Apps 및 Red Hat Instights 가 있음. 

**프라이빗 클라우드(private cloud)**: 특정 기업 그룹에게만 제공되는 클라우드 서비스


**참고자료**
- [완벽한 IT 인프라 구축을 위한 Docker (2판)](https://ebook-product.kyobobook.co.kr/dig/epd/ebook/E000003122038)
- [Iaas/PaaS/SaaS 설명](https://www.redhat.com/ko/topics/cloud-computing/iaas-vs-paas-vs-saas)