# mrrs
会议室预约系统（meeting room reservation system 简称：mrrs）

## 开发环境: 
* vs2017 + qt5.14.0

## 主要功能点：
* <font color=red>**具备用户管理功能。**</font>
    1. 新用户注册。
    2. 用户登录。
    3. 用户信息修改。
    4. 找回密码（提供验证信息）。
    5. 管理员可对用户进行强制注销（适用于离职人员）。
* <font color=red>**具备权限控制。**</font>
    1. 用户类别分为管理员与普通用户。
    2. 管理员可对会议室信息进行增删改查等操作，普通用户只能进行（取消）会议室预约、（取消）参与会议。
* <font color=red>**具备会议室管理功能。**</font>
    1. 会议室管理只能由管理员进行。
    2. 可添加会议室（名称、可用时间、最大容纳人数、描述）。
    3. 可通过指定条件（名称、日期、时间段、可用性）对会议室进行筛选查询。
    4. 可对指定会议室的指定时间段进行（解除）禁用。
    5. 可删除指定会议室。
* <font color=red>**可查看指定日期下的会议室状态。**</font>
    1. 日期通过日历进行选择。
    2. 选择指定日期后可对该日期下所有会议室的状态进行查看（使用甘特图显示状态更直观）。
* <font color=red>**可对指定会议室进行预约。**</font>
    1. 选则指定会议室后进入会议室预约窗口，填写会议室预约信息（会议主题、主持人、参会人员、会议时长、会议简介、会议附件）。
    2. 同一会议室同一时间段只能有一个预约。
    3. 会议室预约完成后，需向参会人员发送会议邀请。
    4. 会议邀请反馈状态需在会议信息中进行展示。
* <font color=red>**可查看当前用户所预约的会议室以及需要参加的会议。**</font>
    1. 用户登录后的主界面分为两部分，会议室预约/我的预约。
    2. 我的预约分为两类，会议室预约及会议预约。
    3. 会议室预约中显示由当前用户预约的会议室。
    4. 会议预约中显示当前用户需要参加的会议，包含主动参与和被邀请后同意的。
    5. 当前时间大于会议室开始使用时间（会议开始时间）但小于会议室结束使用时间（会议结束时间），</br>
       在该条预约信息上“显示会议室使用中（会议进行中）”，当前时间大于会议室结束使用时间（会议结束时间），则该条记录从我的预约中消失。
* <font color=red>**用户可对指定会议进行（取消）参与操作。**</font>
    1. 预约的会议室对外的直观表现为会议，用户可通过操作（鼠标菜单等）实现（取消）参与。
    2. 参加会议需要先向会议组织者（会议室预约者）发送申请，申请通过后，该会议出现在我的预约中。
* <font color=red>**具备会议提醒功能。**</font>
    1. 客户端需要在会议开始前30分钟、10分钟两个时刻对所有参会人员发送通知。
    2. 用户收到参会邀请（申请）时，客户端显示通知。
    3. 申请参与会议反馈（通过/未通过），客户端显示通知。
    4. 所有通知采用类似QQ弹窗的方式通知用户。
    5. 用户可通过系统设置对消息提醒进行（取消）屏蔽操作。
* <font color=red>**显示待处理项**</font>
    1. 显示未处理的参会申请、会议邀请。
    2. 点击待处理项后可对该项进行处理，参会申请处理方式为同意/拒绝，会议邀请处理方式为接受/拒绝，若拒绝可提供理由编辑窗口，并随反馈发送至发起端。
* <font color=red>**可查看历史会议**</font>
    1. 提供当前用户参与的历史会议显示界面，可根据关键词（主题、时间、主持人）进行筛选。
    2. 可查看本次会议纪要及相关会议文件，并提供下载接口。
* <font color=red>**其他**</font>
    1. 用户可通过系统设置对会议邀请的默认处理（时间超过XX分钟未处理则默认为接受/拒绝，或设置全部拒绝/全部接受）。
    2. 会议结束后，预约会议室的用户可上传会议纪要及相关文档，文档存储有两种方式：
        + 文件上传至服务器，服务器将文件存放到本地并将文件路径存放在数据库中，客户端查询时，先获取文件路径，再向服务器发送下载请求从而获取文件。
        + 直接将文件以二进制方式存放到数据库中，下载数据直接从数据库中下载即可。
    3. 定期对数据库进行备份操作，以免数据丢失造成重大损失（针对上条第二种存储方式，会议文档可能很重要）。