# Mybatis-Plus

### 查询

> 查询全部

```
List<RyeDemo> list = demoService.list();
```

> 查询需要某一列的集合

```
List<Long> ids = demoService.listObjs(Wrappers.<RyeDemo>query()
                .select(RyeDemo.ID)
                .eq(RyeDemo.TYPE, 1)
                .groupBy(RyeDemo.NAME)
        , TypeUtils::castToLong);
```

> 查询需要的集合

```
List<RyeDemo> list = demoService.list(Wrappers.<RyeDemo>query()
        			.in(RyeDemo.TYPE, types));
```

> 根据ID查询

```
RyeDemo demo = demoService.getById(1L);
```

> 根据某一列 查一个值

```
EqianbaoContractInput eqianbaoContractInput = eqianbaoContractInputService
        .getOne(Wrappers.<EqianbaoContractInput>query()
                .select()
                .eq(EqianbaoContractInput.ENROLLMENT_ID, requiredInputPARM.getEnrollmentId()));
```

> 根据条件查询对象

```
RyeDemo one = demoService.getOne(Wrappers.<RyeDemo>query()
        .select(RyeDemo.ID, RyeDemo.NAME)
        .eq(RyeDemo.ID, 1L));
```

> 属性名字 一直 两个对象之间填充

```
RyeDemoVO ryeDemoVO = demo.convert(RyeDemoVO.class);
```

> 根据id删除

```
demoService.removeById(1);
```

> 查询 一条记录的 属性值

```
String name = demoService.getObj(Wrappers.<RyeDemo>query()
        .select(RyeDemo.ID), TypeUtils::castToString);
```

> 分页查询一个list

```
Page<TopicReport> pages = topicReportService.page(getPage(), Wrappers.<TopicReport>lambdaQuery()
                .select(TopicReport::getId,
                        TopicReport::getTopicId,
                        TopicReport::getContent,
                        TopicReport::getCreateTime,
                        TopicReport::getCreateUserPhone
                )
                .like(StringUtils.isNotBlank(userName), TopicReport::getCreateUserPhone, userName)
                .eq(Objects.nonNull(topicId), TopicReport::getTopicId, topicId)
                .ge(Objects.nonNull(startTime), TopicReport::getCreateTime, startTime)
                .le(Objects.nonNull(endTime), TopicReport::getCreateTime, endTime)
        );
```

> 分页查询一个list  转换为别的对象  并循环添加其他属性

```
Page<MemberCouponDTO> memberCouponDTOPage =
memberCouponService.page(getPage()).convert(e -> e.convert(MemberCouponDTO.class));

memberCouponDTOPage.getRecords().forEach(e -> {
            e.setUserNumber(memberCouponCodeService.count(Wrappers.<MemberCouponCode>query().eq(MemberCouponCode.MEMBER_COUPON_ID, e.getId()).eq(MemberCouponCode.USED, true)));
        });
```

