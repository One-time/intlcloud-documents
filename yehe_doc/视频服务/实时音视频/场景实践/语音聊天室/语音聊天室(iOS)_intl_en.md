## Demonstration
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo we provide to try out TRTC’s audio chat room features, including seat management, low-latency audio interaction, text chat, etc.


To quickly implement the audio chat room feature, you can modify the demo we provide and adapt it to your needs. You can also use the `TRTCVoiceRoom` component and customize your own UI.

[](id:DemoUI)
## Using the Demo UI

[](id:ui.step1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestVoiceRoom` and click **Create**.

>?This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



[](id:ui.step2)

### Step 2. Download the SDK and demo source code
1. Download the SDK and demo source code for your platform.
2. Click **Next**.
![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)

[](id:ui.step3)
### Step 3. Configure demo project files
1. In the **Modify Configuration** step, select the development platform in line with the source package downloaded.
2. Find and open the `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` file.
3. Set parameters in `GenerateTestUserSig.h`:
	- SDKAPPID: 0 by default. Set it to the actual `SDKAppID`.
	- SECRETKEY: an empty string by default. Set it to the actual key.

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4. Run the demo
Use Xcode (version 11.0 or above) to open the `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace` project and click **Run**.

[](id:ui.step5)
### Step 5. Modify the demo source code
The `TRTCVoiceRoomDemo` folder in the source code contains two subfolders: `ui` and `model`. The `ui` subfolder contains UI code and UI-related logic. The table below lists the Swift files (folders) and the UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
|:-------:|:--------|
|TRTCVoiceRoomEnteryController| The initialization method for all view controllers. You can use the instance to quickly get a `ViewController` object. |
| NetworkRoomManager | Logic for interactions with the business backend |
| TRTCCreateVoiceRoomViewController | Logic for the room creation view |
| TRTCVoiceRoomListViewController | Logic for the room list view |
| TRTCVoiceRoomViewController | Logic for the main room views for room owners and listeners |

Each `TRTC'XXXX'ViewController` folder contains `ViewController`, `RootView`, and `ViewModel`, whose use is described below.

| File | Description |
|:-------:|:--------|
| ViewController | Page controller, which is responsible for routing pages and binding `RootView` and `ViewModel` |
| RootView | Layout of all views |
| ViewModel | View controller, which is responsible for responding to users’ interactions with views and returning response status |

[](id:model)
## Customizing UI
The `TRTCVoiceRoomDemo` folder in the [source code](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCVoiceRoomDemo) contains two subfolders: `ui` and `model`. The `model` folder contains the reusable open-source component `TRTCVoiceRoom`. You can find the component’s APIs in `TRTCVoiceRoom.swift` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/319beb14d72a43120e102380278aa1da.png)


[](id:model.step1)
### Step 1. Integrate the SDKs
The audio chat room component `TRTCVoiceRoom` depends on the TRTC SDK and IM SDK. Follow the steps below to integrate the two SDKs into your project.

**Method 1: adding dependencies via CocoaPods**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?You can view the latest version numbers of the two SDKs by visiting their GitHub pages at [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK).

**Method 2: adding dependencies through local files**
If your access to the CocoaPods repository is slow, you can download the ZIP files of the SDKs and manually integrate them into your project as instructed in the documents below.

| SDK | Download Page | Integration Guide |
|---------|---------|---------|
| TRTC SDK | [Download](https://intl.cloud.tencent.com/document/product/647/34615) | [Integration document](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [Download](https://intl.cloud.tencent.com/document/product/1047/33996) | [Integration document](https://intl.cloud.tencent.com/document/product/1047/34306) |

[](id:model.step2)
### Step 2. Configure permission requests
Configure the mic permission request by adding `Privacy > Microphone Usage Description` in `info.plist`.

[](id:model.step3)
### Step 3. Import the `TRTCVoiceRoom` component
Copy all files in `iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCVoiceRoomDemo/model` to your project.

[](id:model.step4)
### Step 4. Create an instance and log in
1. Call the `sharedInstance` class method of `TRTCVoiceRoom` to create an instance that complies with `TRTCVoiceRoom`’s protocol, or call the `shared` class method to get a `TRTCVoiceRoomImp` instance. There is no difference between the two methods with respect to API usage.
2. Call the `setDelegate` function to register event callbacks of the component.
3. Call the `login` function to log in to the component. Set the key parameters as described below.
<table>    
<tr><th>Parameter</th><th>Description</th></tr><tr>
<td>SDKAppID</td>
<td>You can view the `SDKAppID` of your application in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr><tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_).</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security signature. To obtain one, see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr></tr>
<tr>
<td>callback</td>
<td>Login callback. The code is 0 if login is successful.</td>
</tr></table>
<dx-codeblock>
::: Swift Swift
// Swift example
// The class responsible for business logic in your code
class YourController {
    // Calculate attributes to get a singleton object
    var voiceRoom: TRTCVoiceRoomImp {
        return TRTCVoiceRoomImp.shared()
    }
    
    // Other code logic
    ......
}
// Set a `voiceroom` delegate
self.vocieRoom. setDelegate(delegate: voiceRoomDelegate)

// Below is the calling method. We recommend you use `weak self` in the closure to prevent circular references. The `weak self` part is not included in the sample code below.
self.vocieRoom.login(sdkAppId: sdkAppID, userId: userId, userSig: userSig) { [weak self] (code, message) in
    guard let `self` = self else { return }
    // Your callback business logic        
}
:::
</dx-codeblock>

[](id:model.step5)
### Step 5. Create a room and become a speaker
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Call `createRoom` to create an audio chat room, passing in room-related parameters such as room ID, whether to request your consent for listeners to speak, the number of seats, etc.
3. After creating the room, call `enterSeat` to take a seat.
4. You will receive an `onSeatListChanget` notification about the change of the seat list, and can update the change to the UI.
5. You will also receive an `onAnchorEnterSeat` notification about the occupation of a seat, and mic capturing will be enabled automatically.

![](https://main.qcloudimg.com/raw/256ebe5ce1426b3f175c8c8b68095d5b.png)

Sample code:

```swift
// 1. Set your nickname and profile photo
self.voiceRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // Result callback           
}



// 2. Create a room
let param = VoiceRoomParam.init()
param.roomName = "Room ID"
param.needRequest = true // Whether your consent is required for listeners to speak
param.coverUrl = "Cover URL"
param.seatCount = 7 // Number of room seats. In this example, the number is 7. 6 seats are available after you take one.
param.seatInfoList = []
for _ in 0..<param.seatCount {
    let seatInfo = VoiceRoomSeatInfo.init()
    param.seatInfoList.append(seatInfo)
}
self.voiceRoom.createRoom(roomID: yourRoomID, roomParam: param) { (code, message) in
    guard code == 0 else { reutrn }
    // Take a seat after creating the room
    self.voiceRoom.enterSeat(seatIndex: 0) { [weak self] (code, message) in
        guard let `self` = self else { return }
        if code == 0 {
            // Seat taken successfully
        } else {
            // Failed to take a seat
        }
    }
}



// 3. After taking a seat, you receive an `onSeatListChange` notification
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refresh your seat list
}



// 4. You receive an `onAnchorEnterSeat` notification
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // Handle the seat taking event
}
```

[](id:model.step6)
### Step 6. Enter a room as a listener
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Get the latest audio chat room list from the backend.
 >?The audio chat room list in the demo is for demonstration only. The logic of audio chat room lists varies significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
3. Call `getRoomInfoList` to get short descriptions of the rooms, which are provided by the room owner during room creation via the calling of `createRoom`.
 >!If your audio chat room list already displays enough room information, you can skip the step of calling `getRoomInfoList`.
4. Select an audio chat room, and call `enterRoom` with the room ID passed in to enter the room.
5. After entering the room, you will receive an `onRoomInfoChange` notification about room change from the component. Record the room information, including room name, whether the room owner’s consent is required for listeners to speak, etc., and update it to the UI.
6. You will receive an `onSeatListChange` notification about seat change from the component. Update the change to the UI.
7. You will also receive an `onAnchorEnterSeat` notification about the occupation of a seat.


![](https://main.qcloudimg.com/raw/33432f97eb632fbb9710a59cba9e4469.png)


<dx-codeblock>
::: Swift Swift
// 1. Set your nickname and profile photo
self.voiceRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // Result callback           
}

// 2. Get the room list from the backend. Suppose it is `roomList`.
let roomList: [Int] = getRoomIDList() // The function you use to get the list of room IDs

// 3. Call `getRoomInfoList` to get details of the rooms
self.voiceRoom.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [VoiceRoomInfo]) in
    // Refresh the UI after getting the result
}

// 4. Select an audio chat room, and pass in the `roomId` to enter it
self.voiceRoom.enterRoom(roomID: roomInfo.roomID) { (code, message) in
    // Callback of the room entry result
    if code == 0 {
       // Entered room
    }
}

// 5. After entering the room, you receive an `onRoomInfoChange` notification
func onRoomInfoChange(roomInfo: VoiceRoomInfo) {
    // Update the room name and other information
}

// 6. You receive an `onSeatListChange` notification
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refresh the seat list
}

// 7. You receive an `onAnchorEnterSeat` notification
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // Handle the seat taking event
}
:::
</dx-codeblock>

[](id:model.step7)
### Step 7. Manage seats
<dx-tabs>
::: Room owner
1. A room owner can put a listener in a seat by passing in the `userId` of the listener and the seat number to `pickSeat`. All members in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.
2. A room owner can remove a speaker from a seat by passing in the seat number to `kickSeat`. All members in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.
3. A room owner can mute or unmute a seat by passing in the seat number to `muteSeat`. All members in the room will receive an `onSeatListChange` notification and an `onSeatMute` notification.
4. A room owner can block or unblock a seat by passing in the seat number to `closeSeat`. Listeners cannot take a blocked seat, and all members in the room will receive an `onSeatListChange` notification and an `onSeatClose` notification.
![](https://main.qcloudimg.com/raw/367a0c670d2f9899d0b311ed1f322ea3.png)
:::
::: Listener
1. A listener can take a seat by passing in the seat number to `enterSeat`. All members in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.
2. A listener can leave a seat by calling `leaveSeat`. All members in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

![](https://main.qcloudimg.com/raw/8d385dd387b6255b8512dbff5829e88a.png)

After a seat operation, the order in which different notifications are sent is: callbacks > `onSeatListChange` > independent events such as `onAnchorEnterSeat`.

```Swift
// Case 1: the room owner puts a user in seat 1
self.voiceRoom.pickSeat(seatIndex: 1, userId: "123") { (code, message) in
    // Result callback
}

// 3. The room owner receives an `onSeatListChange` callback, and refreshes the seat list
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refreshed seat list
}

// 4. The room owner receives a notification about the change of a specific seat, which can be used to determine whether the user has taken the seat
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // Handle the seat taking event
}
```

```Swift
// Case 2: a listener takes seat 2
voiceRoom.enterSeat(seatIndex: 2) { (code, message) in
    // Callback of the seat taking result
}

// 3. The listener receives an `onSeatListChange` callback and refreshes the seat list
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refreshed seat list
}

// 4. The listener receives a notification about the change of a specific seat and can determine whether he or she has taken the seat successfully
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // Handle the seat taking event
}
```
:::
</dx-tabs>

[](id:model.step8)
### Step 8. Use signaling for invitations
In [seat management](#model.step7), listeners can take and leave seats without the room owner’s consent, and the room owner can put listeners in seats without the listeners’ consent.
If you want listeners and room owners to obtain each other’s consent before performing the above actions in your application, you can use signaling for invitation sending.
<dx-tabs>
::: Listener requesting to take seat
1. A listener calls `sendInvitation`, passing in information including the room owner’s `userId` and custom command words. The API will return an `inviteId`, which should be recorded.
2. The room owner receives an `onReceiveNewInvitation` notification, and a window pops up on the UI asking the room owner whether to accept the request.
3. The room owner calls `acceptInvitation` with the `inviteId` passed in to accept the request.
4. The listener receives an `onInviteeAccepted` notification and calls `enterSeat` to take a seat.

![](https://main.qcloudimg.com/raw/5ccdb15f63efa127aa883ca6a7bcd80d.png)

<dx-codeblock>
::: Swift Swift
// Listener
// 1. Call `sendInvitation` to request to take seat 1
let inviteId = self.voiceRoom.sendInvitation(cmd: "ENTER_SEAT", userId: ownerUserId, content: "1") { (code, message) in
    // Callback of the request sending result
}
// 2. Take the seat when the request is accepted by the room owner
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.voiceRoom.enterSeat(seatIndex: ) { (code, message) in
            // Callback of the seat taking result
        }
    }
}

// Room owner
// 1. Receive the request
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 2. Accept the request
        self.voiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
:::
</dx-codeblock>
:::
::: Room owner inviting listener to take seat
1. The room owner calls `sendInvitation`, passing in information including the listener's `userId` and custom command words. The API will return an `inviteId`, which should be recorded.
2. The listener receives an `onReceiveNewInvitation` notification, and a window pops up asking the listener whether to agree to speak.
3. The listener calls `acceptInvitation` with the `inviteId` passed in to accept the invitation.
4. The room owner receives an `onInviteeAccepted` notification and calls `pickSeat` to put the listener in a seat.

![](https://main.qcloudimg.com/raw/5515f49d6e30410e12cd828b75a8db0b.png)


<dx-codeblock>
::: java java
// Room owner
// 1. Call `sendInvitation` to invite user `123` to take seat 2
let inviteId = self.voiceRoom.sendInvitation(cmd: "PICK_SEAT", userId: ownerUserId, content: "2") { (code, message) in
    // Callback of the request sending result
}

// 2. Put the user in the seat when the invitation is accepted by the listener
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.voiceRoom.pickSeat(seatIndex: ) { (code, message) in
            // Callback of the seat taking result
        }
    }
}

// Listener
// 1. Receive the request
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 2. Accept the request
        self.voiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
:::
</dx-codeblock>
:::
</dx-tabs>

[](id:model.step9)
### Step 9. Enable text chat and on-screen comments
- Call `sendRoomTextMsg` to send common text messages. All users in the room will receive an `onRecvRoomTextMsg` callback.
IM has its default content moderation rules. Text messages that contain restricted terms will not be forwarded by the cloud.
<dx-codeblock>
::: Swift Swift
// Sender: send text messages
self.voiceRoom.sendRoomTextMsg(message: message) { (code, message) in
         

}
// Recipient: listen for text messages
func onRecvRoomTextMsg(message: String, userInfo: VoiceRoomUserInfo) {
    // Handling of the messages received        
}
:::
</dx-codeblock>
- Call `sendRoomCustomMsg` to send custom (signaling) messages. All users in the room will receive an `onRecvRoomCustomMsg` callback.
 Custom messages are often used to transfer custom signals, e.g., giving and broadcasting likes.
<dx-codeblock>
::: Swift Swift
// For example, a sender can customize commands to distinguish on-screen comments and likes
// For example, use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes
self.vocieRoom.sendRoomCustomMsg(cmd: “CMD_DANMU”, message: "hello world", callback: nil)
self.voiceRoom.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)
// Recipient: listen for custom messages
func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: VoiceRoomUserInfo) {
    if cmd == "CMD_DANMU" {
        // Receive an on-screen comment
    }
    if cmd == "CMD_LIKE" {
        // Receive a like
    }
}
:::
</dx-codeblock>

