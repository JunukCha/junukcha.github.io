---
layout: post
title: SMPL:Human mesh model
tags: [basic, human, mesh]
published: false
category: test
math: true
---

## Human mesh
인공지능과 컴퓨터 비전 분야에서 인간의 신체를 정확하고 현실적으로 모델링하는 것은 매우 중요한 과제입니다. 이러한 맥락에서, SMPL(Skinned Multi-Person Linear Model)은 혁신적인 접근 방식을 제시합니다. **SMPL**은 3차원 인간 신체 모델링을 위한 Parameteric 모델로, 신체의 **형태(Shape)**와 **포즈(Pose)**를 모두 포괄적으로 표현할 수 있습니다. 이 모델은 신체의 다양한 형태와 동작을 수학적으로 정의함으로써, 가상 환경에서 인간의 신체를 자연스럽고 사실적으로 재현할 수 있는 능력을 제공합니다. 본 글에서는 SMPL의 기본 원리와 구조, 그리고 이 모델이 어떻게 다양한 응용 분야에서 중요한 역할을 하는지에 대해 살펴보고자 합니다.

## 입력과 출력
Human mesh를 생성하는 SMPL 모델은 크게 2가지의 입력 파라미터를 받습니다. 첫 번째, 형태(Shape) 파라미터입니다. 이 파라미터는 베타 ($\beta$)로 표현하며 10개의 값을 가지고 있습니다. ($\beta \in \mathbb{R}^{10}$). 이 파라미터는 사람의 체형을 나타내는 파라미터로 