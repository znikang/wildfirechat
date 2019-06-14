# General FAQ

## 1. 如何处理信息托管
A：野火IM提供了群组托管/用户信息托管/好友关系托管。对这3种信息采用不同的处理方式
1. 群组托管必须使用野火IM的。
2. 用户信息托管是可选的。当选择野火IM托管时，客户可以使用服务API向野火IM同步用户信息（用户信息会自动同步到客户端)。当不托管时，可以在客户端实现```UserSource```，满足我们声明的接口（协议）后，IMUIKIT可以正常使用。
3. 好友关系托管可选。当选择好友关系托管时，好友关系建议仅使用野火IM的，不建议使用同步方案。当不托管时，客户需要自己来实现好友关系的相关UI。野火IM的消息发送不依赖于好友关系。由于好友关系相对独立，因此比较容易解决UI问题。建议客户自己来处理好友关系。

## 2. 为什么删除了好友关系还能发送消息
A：野火IM发送消息时不对用户关系进行判断，只有有对方ID就可以发送（黑名单除外），因此陌生人或者删除好友都可以继续发送消息。如果需要控制，请在应用层进行控制。

## 3. 为啥发送好友请求后不能再次发送好友请求
A：为了防止稍扰，野火IM对好友请求做了以下规定
1. 如果以前没有发送过好友请求，可以发送好友请求。
2. 如果以前发送过好友请求，对方已经接受了，可以再次发送请求。
3. 如果以前发送过好友请求，对方没有处理，在7天内会报错已经发送过，7天之后可以再次发送。
4. 如果以前发送过好友请求，对方拒绝，在30天内再次发送会报错已经被拒绝，30天之后可以再次发送。

## 4. 用户信息的更新策略
Q：用户的头像更新了，为什么我这一端还显示旧头像？
A：用户信息不是强同步的（强同步的有消息，好友列表，各种设置），因为要实现用户信息强同步需要付出非常大的代价，因此一般是不自动更新用户信息，只有在特定的情况下才去更新。野火IM在与某用户单聊时会强制更新一下该用户的用户信息，还有在该用户的个人详情页面也会更新，基本与微信/QQ逻辑一致。如果客户需要在特定的界面更新，可以自己修改对于的源码，获取用户信息时强制更新即可。