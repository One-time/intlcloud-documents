`TRTCChorusRoom` is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). Its features include:

- A user can create a room and start streaming as the room owner, or enter a room as audience to listen or sing together with the room owner.
- The room owner can manage song requests, invite a listener to speak, remove a speaker, and start a duet.
- The room owner can also block a seat. Listeners cannot request to take a blocked seat.
- A listener can request to sing and become the co-singer, and the co-singer can become a listener after a duet ends.
- All users can send gifts and text and custom messages. Custom messages can be used to send on-screen comments and give likes.

`TRTCChorusRoom` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Duet (Android)](https://intl.cloud.tencent.com/document/product/647/42689).

- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio chat component.
- IM SDK: the `AVChatRoom` feature of the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to implement chat rooms. The attribute APIs of IM are used to store room information such as the seat list, and invitation signaling is used to send requests to speak or invite others to speak.

[](id:TRTCChorusRoom)
## `TRTCChorusRoom` API Overview

### Basic SDK APIs

| API                                             | Description                                                         |
| --------------------------- | ---- |
| [sharedInstance](#sharedinstance) | Gets a singleton object. |
| [destroySharedInstance](#destroysharedinstance) | Terminates a singleton object. |
| [setDelegate](#setdelegate) | Sets event callbacks. |
| [setDelegateHandler](#setdelegatehandler) | Sets the thread where event callbacks are. |
| [login](#login)                   | Logs in.                   |
| [logout](#logout)                 | Logs out.                   |
| [setSelfProfile](#setselfprofile) | Sets the profile. |

### Room APIs

| API                                             | Description                                                         |
| --------------- | -------------------- |
| [createRoom](#createroom) | Creates a room (called by room owner). If the room does not exist, the system will automatically create a room. |
| [destroyRoom](#destroyroom) | Terminates a room (called by room owner). |
| [enterRoom](#enterroom) | Enters a room (called by listener). |
| [exitRoom](#exitroom) | Exits a room (called by listener). |
| [getRoomInfoList](#getroominfolist) | Gets room list details.                                     |
| [getUserInfoList](#getuserinfolist) | Gets the user information of the specified `userId`. If the value is `null`, the information of all users in the room is obtained. |

### Music playback APIs

| API                                             | Description                                                         |
| --------------- | --------------- |
| [startPlayMusic](#startPlayMusic) | Starts music playback.     |
| [stopPlayMusic](#stopPlayMusic) | Stops music playback.     |
| [pausePlayMusic](#pausePlayMusic) | Pauses music playback.     |
| [resumePlayMusic](#resumePlayMusic) | Resumes music playback.     |

### Seat management APIs

| API     | Description |
| ----------------------- | ----------------- |
| [enterSeat](#enterseat) | Becomes a speaker (called by room owner or listener). |
| [leaveSeat](#leaveseat) | Becomes a listener (called by speaker).    |
| [pickSeat](#pickseat)   | Places a user in a seat (called by room owner).                  |
| [kickSeat](#kickseat)   | Removes a speaker (called by room owner).                  |
| [closeSeat](#closeseat) | Blocks/Unblocks a seat (called by room owner).          |

### Local audio APIs

| API                                             | Description                                                         |
| --------------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | Starts mic capturing.     |
| [stopMicrophone](#stopmicrophone)               | Stops mic capturing.     |
| [setAudioQuality](#setaudioquality)             | Sets audio quality.           |
| [muteLocalAudio](#mutelocalaudio)               | Mutes/Unmutes local audio.       |
| [setSpeaker](#setspeaker)                       | Sets whether to use the speaker or receiver.     |
| [setAudioCaptureVolume](#setaudiocapturevolume) | Sets mic capturing volume. |
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | Sets playback volume. |
| [setVoiceEarMonitorEnable](#setvoiceearmonitorenable) | Enables/Disables in-ear monitoring.       |


### Remote audio APIs

| API                                             | Description                                                         |
| --------------------- | -------------------- |
| [muteRemoteAudio](#muteremoteaudio)       | Mutes/Unmutes a specified member. |
| [muteAllRemoteAudio](#muteallremoteaudio) | Mutes/Unmutes all members. |

### Background music and audio effect APIs

| API                                             | Description                                                         |
| --------------------------- | -------------------- |
| [getAudioEffectManager](#getaudioeffectmanager) | Gets the background music and audio effect management object [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__android.html#interfacecom_1_1tencent_1_1liteav_1_1audio_1_1TXAudioEffectManager). |

### Message sending APIs

| API                                             | Description                                                         |
| ------------------- | -------------------- |
| [sendRoomTextMsg](#sendroomtextmsg) | Broadcasts a text message in a room. This API is generally used for on-screen comments. |
| [sendRoomCustomMsg](#sendroomcustommsg) | Sends a custom text message. |

### Invitation signaling APIs

| API                                             | Description                                                         |
| ----------------- | ---------------- |
| [sendInvitation](#sendinvitation)     | Sends an invitation. |
| [acceptInvitation](#acceptinvitation) | Accepts an invitation.       |
| [rejectInvitation](#rejectinvitation) | Declines an invitation.       |
| [cancelInvitation](#cancelinvitation) | Cancels an invitation.       |

<h2 id="TRTCChorusRoomDelegate">`TRTCChorusRoomDelegate` API Overview</h2>

### Common event callback APIs

| API                                             | Description                                                         |
| ----- | ---------- |
| [onError](#onerror) | Error|
| [onWarning](#onwarning) | Warning|
| [onDebugLog](#ondebuglog) | Log|

### Room event callback APIs

| API                                             | Description                                                         |
| --------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy)     | The room was terminated.       |
| [onRoomInfoChange](#onroominfochange)     | The room information changed. |
| [onUserVolumeUpdate](#onuservolumeupdate) | User volume     |

### Seat list change callback APIs

| API     | Description |
| ------------------- | --------------- |
| [onSeatListChange](#onseatlistchange)   | All seat changes                |
| [onAnchorEnterSeat](#onanchorenterseat) | Someone became a speaker or was made a speaker by the room owner. |
| [onAnchorLeaveSeat](#onanchorleaveseat) | Someone became a listener or was moved to listeners by the room owner. |
| [onSeatMute](#onseatmute) | The room owner muted/unmuted a seat. |
| [onUserMicrophoneMute](#onusermicrophonemute) | Whether a user’s mic is muted|

| [onSeatClose](#onseatclose)             | The room owner blocked/unblocked a seat.                          | 

### Callback APIs for room entry/exit by listener

| API                                             | Description                                                         |
| --------------- | ------------------ |
| [onAudienceEnter](#onaudienceenter) | A listener entered the room. |
| [onAudienceExit](#onaudienceexit) | A listener exited the room. |

### Message event callback APIs

| API                                             | Description                                                         |
| ----------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | A text message was received.|
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | A custom message was received.|

## Signaling Event Callback APIs

| API                                             | Description                                                         |
| --------- | ---------------- |
| [onReceiveNewInvitation](#onreceivenewinvitation) | A new invitation was received.   |
| [onInviteeAccepted](#oninviteeaccepted)           | The invitee accepted the invitation.   |
| [onInviteeRejected](#oninviteerejected)           |  The invitee declined the invitation.   |
| [onInvitationCancelled](#oninvitationcancelled)   | The inviter canceled the invitation. |

### Song event callback APIs

| API                                             | Description                                                         |
| --------- | ----------------- |
| [onMusicProgressUpdate](#onMusicProgressUpdate) | Music playback progress |
| [onMusicPrepareToPlay](#onMusicPrepareToPlay) | Music playback is ready. |
| [onMusicCompletePlaying](#onMusicCompletePlaying) | Music playback was completed. |
| [onReceiveAnchorSendChorusMsg](#onReceiveAnchorSendChorusMsg) | The room owner sent a duet message. |

## Basic SDK APIs

<span id="sharedInstance"></span>

### sharedInstance

This API is used to get a [TRTCChorusRoom](https://intl.cloud.tencent.com/document/product/647/41941) singleton object.

```java
 public static synchronized TRTCChorusRoom sharedInstance(Context context);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------- | -------------------- |
| context | Context | Android context, which will be converted to `ApplicationContext` for the system APIs to call. |

   

### destroySharedInstance

This API is used to terminate a [TRTCChorusRoom](https://intl.cloud.tencent.com/document/product/647/41941) singleton object.

>?After the instance is terminated, the externally cached `TRTCChorusRoom` instance can no longer be used. You need to call [sharedInstance](#sharedinstance) again to get a new instance.

```java
public static void destroySharedInstance();
```

### setDelegate

This API is used to set the event callbacks of [TRTCChorusRoom](https://intl.cloud.tencent.com/document/product/647/41941). You can use `TRTCChorusRoomDelegate` to get different status notifications of [TRTCChorusRoom](https://intl.cloud.tencent.com/document/product/647/41941).

```java
public abstract void setDelegate(TRTCChorusRoomDelegate delegate);
```

>?`setDelegate` is the delegate callback of `TRTCChorusRoom`.   

### setDelegateHandler

This API is used to set the thread where event callbacks are.

```java
public abstract void setDelegateHandler(Handler handler);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------- | -------------------- |
| handler | Handler | The status notifications of `TRTCChorusRoom` are sent to the handler thread you specify. |

   

### login

Login

```java
public abstract void login(int sdkAppId,
 String userId, String userSig,
TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | -------------------- |
| sdkAppId | int | You can view `SDKAppID` in **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info** of the TRTC console. |
| userId | String | ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (\_) |
| userSig | String | Tencent Cloud's proprietary security signature. For how to obtain it, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| callback | ActionCallback | Callback for login. The code is `0` if login succeeds. |

   

### logout

This API is used to log out.

```java
public abstract void logout(TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | ------- |
| callback | ActionCallback | Callback for logout. The code is `0` if logout succeeds. |

   

### setSelfProfile

This API is used to set the profile.

```java
public abstract void setSelfProfile(String userName, String avatarURL, TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| --------- | -------------- | --------------- |
| userName | String | Username|
| avatarURL | String | Profile photo URL |
| callback | ActionCallback | Callback for profile setting. The code is `0` if the operation succeeds. |

   


## Room APIs

### createRoom

This API is used to create a room (called by room owner).

```java
public abstract void createRoom(int roomId, TRTCChorusRoomDef.RoomParam roomParam, TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ------------------- | -------------------- |
| roomId | int | Room ID. You need to assign and manage the IDs in a centralized manner. Multiple `roomID` values can be aggregated into a room list. Currently, Tencent Cloud does not provide management services for room lists. Please manage the list on your own. |
| roomParam | TRTCChorusRoomParam | Room information, such as room name, seat list information, and cover information. To manage seats, you must enter the number of seats in the room. |
| callback | ActionCallback | Callback for room creation. The code is `0` if the operation succeeds.  |

The process of creating a room and becoming a speaker is as follows: 
1. A user calls `createRoom` to create a room, passing in room attributes (e.g., room ID, whether listeners need room owner’s consent to speak, number of seats).
2. After creating the room, the user calls `enterSeat` to become a speaker.
3. The user will receive an `onSeatListChanget` notification about the change of the seat list, and can update the change to the UI.
4. The user will also receive an `onAnchorEnterSeat` notification that someone became a speaker, and mic capturing will be enabled automatically.

   

### destroyRoom

This API is used to terminate a room (called by room owner).

```java
public abstract void destroyRoom(TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ----------------- |
| callback | ActionCallback | Callback for room termination. The code is `0` if the operation succeeds. |


### enterRoom

This API is used to enter a room (called by listener).

```java
public abstract void enterRoom(int roomId, TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ----------------- |
| roomId | int | Room ID |
| callback | ActionCallback | Callback for room entry. The code is `0` if the operation succeeds. |


The process of entering a room as a listener is as follows: 

1. A user gets the latest room list from your server. The list may contain the `roomId` and room information of multiple rooms.
2. The user selects a room, and calls `enterRoom` with the room ID passed in to enter.
3. After entering the room, the user receives an `onRoomInfoChange` notification about room attribute change from the component. The attributes can be recorded, and corresponding changes can be made to the UI, including room name, whether room owner’s consent is required for listeners to speak, etc.
4. The user will receive an `onSeatListChange` notification about the change of the seat list and can update the change to the UI.
5. The user will also receive an `onAnchorEnterSeat` notification that someone became a speaker.

### exitRoom

This API is used to exit a room.

```java
public abstract void exitRoom(TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ----------------- |
| callback | ActionCallback | Callback for room exit. The code is `0` if the operation succeeds. |

   

### getRoomInfoList

This API is used to get room list details. The room name and cover are set by the room owner via `roomInfo` when calling `createRoom()`.

>?You don’t need this API if both the room list and room information are managed on your server.


```java
public abstract void getRoomInfoList(List<Integer> roomIdList, TRTCChorusRoomCallback.RoomInfoCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------------------- | ------------------ |
| roomIdList | List&lt;Integer&gt; | Room ID list |
| callback | RoomInfoCallback | Callback of room details |


### getUserInfoList

This API is used to get the user information of a specified `userId`.

```java
public abstract void getUserInfoList(List<String> userIdList, TRTCChorusRoomCallback.UserListCallback userlistcallback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------------- | ------------------ | -------------------- |
| userIdList       | List&lt;String&gt; | IDs of the users to query. If this parameter is `null`, the information of all users in the room is queried. |
| userlistcallback | UserListCallback   | Callback of user details                                           |

## Music Playback APIs

### startPlayMusic

This API is used to play music (called after mic-on).
>?
>- After music playback starts, you will receive an `onMusicPrepareToPlay` notification.
>- During music playback, all members in the room will keep receiving an `onMusicProgressUpdate` notification.
>- After music playback stops, you will receive an `onMusicCompletePlaying` notification.

```java
public abstract void startPlayMusic(int musicID, String url);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | -------------- | -------------------- |
| musicID | int | Music ID |
| url     | String  | Absolute path of the music track |

After this API is called, the song being played will stop.

### stopPlayMusic

This API is used to stop music (called during music playback).
>?After music playback stops, you will receive an `onMusicCompletePlaying` notification.

```java
public abstract void stopPlayMusic();
```

### pausePlayMusic

This API is used to pause music (called during music playback).
>?
>- The `onMusicProgressUpdate` notification will be paused.
>- No `onMusicCompletePlaying` notification will be received.

```java
public abstract void pausePlayMusic();
```

### resumePlayMusic

This API is used to resume music (called after pause).
>?No `onMusicPrepareToPlay` notification will be received.

```java
public abstract void resumePlayMusic();
```

## Seat Management APIs

### enterSeat

This API is used to become a speaker (called by room owner or listener).

>?After a user becomes a speaker, all members in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.

```java
public abstract void enterSeat(int seatIndex, TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | -------------- | -------------------- |
| seatIndex | int            | The number of the seat to take |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list. In cases where listeners need the room owner’s consent to speak, you can call `sendInvitation` first to send a request and, after receiving `onInvitationAccept`, call `enterSeat`.

### leaveSeat

This API is used to become a listener (called by speaker).

>? After a speaker becomes a listener, all members in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

```java
public abstract void leaveSeat(TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | ---------- |
| callback | ActionCallback | Callback for the operation |

### pickSeat

This API is used to place a user in a seat (called by room owner).

>? After the room owner places a user in a seat, all members in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.

```java
public abstract void pickSeat(int seatIndex, String userId, TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | -------------- | ---------------------- |
| seatIndex | int            | The number of the seat to place the listener in |
| userId | String | User ID |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list. In cases where the room owner needs listeners’ consent to make them speakers, you can call `sendInvitation` first to send a request and, after receiving `onInvitationAccept`, call `pickSeat`.


### kickSeat

This API is used to remove a speaker (called by room owner).

>? After a speaker is removed, all members in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

```java
public abstract void kickSeat(int seatIndex, TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | -------------- | ---------------------- |
| seatIndex | int            | The number of the seat to remove the speaker from |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list.

### muteSeat

This API is used to mute/unmute a seat (called by room owner).

>? After a seat is muted/unmuted, all members in the room will receive an `onSeatListChange` notification and an `onSeatMute` notification.

```java
public abstract void muteSeat(int seatIndex, boolean isMute, TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | -------------- | ------------------------- |
| seatIndex | int            | The number of the seat to mute/unmute                          |
| isMute    | boolean        | `true`: mute; `false`: unmute |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list. The speaker on the seat specified by `seatIndex` will call `muteAudio` to mute/unmute his or her audio.

### closeSeat

This API is used to block/unblock a seat (called by room owner).

>? After a seat is blocked/unblocked, all members in the room will receive an `onSeatListChange` notification and an `onSeatClose` notification.

```java
public abstract void closeSeat(int seatIndex, boolean isClose, TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | -------------- | ---------------------- |
| seatIndex | int            | The number of the seat to block/unblock                          |
| isClose   | boolean        | `true`: block; `false`: unblock |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list. The speaker on the seat specified by `seatIndex` will leave the seat.


## Local Audio APIs

### startMicrophone

This API is used to start mic capturing.

```java
public abstract void startMicrophone();
```

### stopMicrophone

This API is used to stop mic capturing.

```java
public abstract void stopMicrophone();
```

### setAudioQuality

This API is used to set audio quality.

```java
public abstract void setAudioQuality(int quality);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ---- | -------------------- |
| quality | int | Audio quality. For more information, please see [setAudioQuality()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55). |


### muteLocalAudio

This API is used to mute/unmute local audio.

```java
public abstract void muteLocalAudio(boolean mute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------- | -------------------- |
| mute | boolean | Whether to mute or unmute audio. For more information, please see [muteLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86). |



### setSpeaker

This API is used to set whether to use the speaker or receiver.

```java
public abstract void setSpeaker(boolean useSpeaker);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------- | ------- |
| useSpeaker | boolean | `true`: speaker; `false`: receiver |



### setAudioCaptureVolume

This API is used to set the mic capturing volume.

```java
public abstract void setAudioCaptureVolume(int volume);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | --------- |
| volume | int | Capturing volume. Value range: 0-100 (default: 100) |


### setAudioPlayoutVolume

This API is used to set the playback volume.

```java
public abstract void setAudioPlayoutVolume(int volume);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | ------- |
| volume | int | Playback volume. Value range: 0-100 (default: 100) |

### muteRemoteAudio

This API is used to mute/unmute a specified user.

```java
public abstract void muteRemoteAudio(String userId, boolean mute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------- | ------------- |
| userId | String | User ID |
| mute | boolean | `true`: mute; `false`: unmute |

### muteAllRemoteAudio

This API is used to mute/unmute all users.

```java
public abstract void muteAllRemoteAudio(boolean mute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------- | ------------- |
| mute | boolean | `true`: mute; `false`: unmute |

### setVoiceEarMonitorEnable

This API is used to enable/disable in-ear monitoring.

```java
public abstract void setVoiceEarMonitorEnable(boolean enable);
```
The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------- | ------------- |
| enable | boolean | `true`: enable; `false`: disable |


## Background Music and Audio Effect APIs

### getAudioEffectManager

This API is used to get the background music and audio effect management object [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa).

```java
public abstract TXAudioEffectManager getAudioEffectManager();
```


## Message Sending APIs

### sendRoomTextMsg

This API is used to broadcast a text message in a room, which is generally used for on-screen comments.

```java
public abstract void sendRoomTextMsg(String message, TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | -------------- |
| message      | String           | Text message                   |
| callback | ActionCallback | Callback for the operation |

   

### sendRoomCustomMsg

This API is used to send a custom text message.

```java
public abstract void sendRoomCustomMsg(String cmd, String message, TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | ---------- |
| cmd | String | Custom command word used to distinguish between different message types |
| message      | String           | Text message                   |
| callback | ActionCallback | Callback for the operation |

   

## Invitation Signaling APIs

### sendInvitation

This API is used to send an invitation.

```java
public abstract String sendInvitation(String cmd, String userId, String content, TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | ---------------- |
| cmd      | String         | Custom command of business |
| userId   | String         | Invitee’s user ID  |
| content  | String         | Invitation content     |
| callback | ActionCallback | Callback for the operation |

Response parameters:

| Returned Value | Type | Description |
| -------- | ------ | --------------------- |
| inviteId | String | Invitation ID |

### acceptInvitation

This API is used to accept an invitation.

```java
public abstract void acceptInvitation(String id, TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | -------------- |
| id   | String | Invitation ID |
| callback | ActionCallback | Callback for the operation |

### rejectInvitation

This API is used to decline an invitation.

```java
public abstract void rejectInvitation(String id, TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------ | -------- |
| id   | String | Invitation ID |
| callback | ActionCallback | Callback for the operation |


### cancelInvitation

This API is used to cancel an invitation.

```java
public abstract void cancelInvitation(String id, TRTCChorusRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | -------------- |
| id   | String | Invitation ID |
| callback | ActionCallback | Callback for the operation |

[](id:TRTCChorusRoomDelegate)
## `TRTCChorusRoomDelegate` Event Callback APIs

## Common Event Callback APIs

### onError

Callback for error.

>? This callback indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users if necessary.

```java
void onError(int code, String message);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| code | int | Error code |
| message | String | Error message |


### onWarning

Callback for warning.

```java
void onWarning(int code, String message);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| code | int | Error code |
| message | String | Warning message |

   

### onDebugLog

Callback for log.

```java
void onDebugLog(String message);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| message | String | Log information |

   


## Room Event Callback APIs

### onRoomDestroy

Callback for room termination. When the owner terminates the room, all users in the room will receive this callback.

```java
void onRoomDestroy(String roomId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | --------- |
| roomId | String | Room ID |


### onRoomInfoChange

Callback for change of room information. This callback is sent after successful room entry. The information in `roomInfo` is passed in by the room owner during room creation.

```java
void onRoomInfoChange(TRTCChorusRoomDef.RoomInfo roomInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| roomInfo | RoomInfo | Room information |

   

### onUserMicrophoneMute

Callback of whether a user’s mic is muted. When a user calls `muteLocalAudio`, all members in the room will receive this callback.

```java
void onUserMicrophoneMute(String userId, boolean mute);

```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ----- |
| userId | String | User ID |
| mute | boolean    | Volume. Value range: 0-100 |

### onUserVolumeUpdate

Callback of the volume of each member in the room after the volume reminder is enabled.

```java
void onUserVolumeUpdate(List<TRTCCloudDef.TRTCVolumeInfo> userVolumes, int totalVolume);

```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ----- |
| userVolumes | List | List of user volumes                 |
| totalVolume | int    | Total volume. Value range: 0-100 |


## Seat Callback APIs

### onSeatListChange

Callback for all seat changes.

```java
void onSeatListChange(List<SeatInfo> seatInfoList);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | -------------- | ---------------- |
| seatInfoList | List&lt;SeatInfo&gt; | Full seat list |

### onAnchorEnterSeat
Someone became a speaker or was made a speaker by the room owner.

```java
void onAnchorEnterSeat(int index, TRTCChorusRoomDef.UserInfo user);
```
The parameters are as detailed below:

| Parameter | Type | Description |
| ----- | -------- | -------------------- |
| index | int      | The seat taken     |
| user | UserInfo | Details of the user who took the seat |

### onAnchorLeaveSeat

A speaker became a listener or was moved to listeners by the room owner.

```java
void onAnchorLeaveSeat(int index, TRTCChorusRoomDef.UserInfo user);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ----- | -------- | -------------------- |
| index | int      | The seat previously occupied by the speaker         |
| user | UserInfo | Details of the user who became a listener |

### onSeatMute

The room owner muted/unmuted a seat.

```java
void onSeatMute(int index, boolean isMute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------- | -------------- |
| index  | int     | The seat muted/unmuted                       |
| isMute | boolean | `true`: muted; `false`: unmuted |

### onSeatClose

The room owner blocked/unblocked a seat.

```java
void onSeatClose(int index, boolean isClose);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------- | --------------- |
| index   | int     | The seat blocked/unblocked                        |
| isClose | boolean | `true`: blocked; `false`: unblocked |

## Callback APIs for Room Entry/Exit by Listener

### onAudienceEnter

A listener entered the room.

```java
void onAudienceEnter(TRTCChorusRoomDef.UserInfo userInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | -------------- |
| userInfo | UserInfo | Information of the listener who entered the room |

### onAudienceExit

A listener exited the room.

```java
void onAudienceExit(TRTCChorusRoomDef.UserInfo userInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | -------------- |
| userInfo | UserInfo | Information of the listener who exited the room |

   

## Message Event Callback APIs

### onRecvRoomTextMsg

A text message was received.

```java
void onRecvRoomTextMsg(String message, TRTCChorusRoomDef.UserInfo userInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------------- |
| message      | String           | Text message                   |
| userInfo | UserInfo | Information of the sender |

   

### onRecvRoomCustomMsg

A custom message was received.

```java
void onRecvRoomCustomMsg(String cmd, String message, TRTCChorusRoomDef.UserInfo userInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| command | String | Custom command word used to distinguish between different message types |
| message      | String           | Text message                   |
| userInfo | UserInfo | Information of the sender |

## Invitation Signaling Callback APIs

### onReceiveNewInvitation

An invitation was received.

```java
void onReceiveNewInvitation(String id, String inviter, String cmd, String content);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | -------- | -------------- |
| id   | String | Invitation ID |
| inviter | String | Inviter’s user ID |
| cmd     | String   | Custom command word specified by business |
| content | UserInfo | Content specified by business                   |

### onInviteeAccepted

The invitee accepted the invitation.

```java
void onInviteeAccepted(String id, String invitee);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------------- |
| id   | String | Invitation ID |
| invitee | String | Invitee’s user ID |

### onInviteeRejected

The invitee declined the invitation.

```java
void onInviteeRejected(String id, String invitee);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------------- |
| id   | String | Invitation ID |
| invitee | String | Invitee’s user ID |

### onInvitationCancelled

The inviter canceled the invitation.

```java
void onInvitationCancelled(String id, String inviter);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ----------------- |
| id   | String | Invitation ID |
| inviter | String | Inviter’s user ID |

## Music Playback Status Callback APIs

### onMusicPrepareToPlay

Music playback is ready.

```java
void onMusicPrepareToPlay(int musicID);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ---- | -------------------- |
| musicID | int | `musicID` passed in for playback  |

### onMusicProgressUpdate

Music playback progress.

```java
void onMusicProgressUpdate(int musicID, long progress, long total);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ---- | -------------------- |
| musicID | int | `musicID` passed in for playback  |
| progress | long | Current playback progress in ms |
| total    | long | Total duration in ms      |

### onMusicCompletePlaying

Music playback was completed.

```java
void onMusicCompletePlaying(int musicID);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----- | -------------------- |
| musicID | int | `musicID` passed in for playback  |

### onReceiveAnchorSendChorusMsg

The room owner sent a duet message.


```java
void onReceiveAnchorSendChorusMsg(String musicID, long startDelay);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | --------- | -------------------- |
| musicID | String | `musicID` of the song to sing |
| startDelay | long | Time (s) to wait before the song is played  |
