---
title: Launch Snipping Tool
description: This topic describes how to use the new protocol launch framework for Snipping Tool. Your app can use these URI schemes to launch the Snipping Tool capture overlay to create a new snip or recording.
ms.date: 02/14/2025
ms.topic: concept-article
keywords: windows 11, uri, snipping tool, capture
ms.localizationpriority: medium
ms.custom: RS5
# customer-intent: As a Windows developer, I want to learn about the ms-screenclip URI scheme so that I can integrate it into my application to programmatically launch the Snipping Tool. This will allow my application to trigger a snip experience directly, enabling users to take screenshots seamlessly without manually opening the Snipping Tool.
---

# Launch Snipping Tool

This article specifies the protocol for integrating first and third-party applications with the Windows Snipping Tool using the **ms-clip:** URI (Uniform Resource Identifier) scheme. The protocol facilitates the capture of images and video with audio via the Snipping Tool. App callers can customize and choose which Snipping Tool features their app will display. The protocol is designed to offer flexibility, security, and ease of use, aligning closely with familiar HTTP-based interactions. This shift can make the protocol more intuitive for developers and facilitate its integration with web technologies.

> [!NOTE]
> This protocol launch replaces the previous existing experience documented [here](launch-screen-snipping.md).

## Supported features

The Snipping Tool protocol supports the following features:

- Rectangle Capture
- Freeform Capture
- Window Capture
- Ability to launch directly into a Snip or Recording
- Customizing features available
- Autosave feature is available, but can be disabled

## Protocol Specification

**URI Scheme:** `{scheme}://{host}/{path}?{query}`

**ms-screenclip:** takes the following parameters:

- **Scheme:** `ms-screenclip` - The custom scheme for the Snipping Tool protocol.
- **Host:** Specifies the type of capture, e.g. capture, annotate.
- **Path:** The media type being captured or annotated. /image, /video, /audio.
- **Query:** Parameters for the specified schema.

## Host (required)

- Capture

## Path (required)

- Image
- Video

## EnabledModes parameter

The enabledModes parameter is designed to give developers granular control over the available UI options when invoking the ms-screenclip protocol. This allows for a tailored user experience that matches the specific requirements of the calling application. By specifying the enabledModes parameter, developers can restrict the user's choices in the Snipping Tool UI to ensure the output format meets their expectations.

> [!NOTE]
> The FullScreenSnip mode is not supported in interactive mode at this time and should not be included in the enabledModes parameter.

## Supported modes

The **enabledModes** parameter can accept the following modes:

- **RectangleSnip:** Enables rectangle capture mode.
- **WindowSnip:** Enables window capture mode.
- **FreeformSnip:** Enables freeform capture mode.
- **RectangleRecord:** Enables rectangle recording mode.
- **RecordAllModes:** Enables all recording modes (currently only RectangleRecord is available).
- **SnippingAllModes:** Enables all snipping (image capture) modes (RectangleSnip, WindowSnip, FreeformSnip).
- **All:** Enables all supported modes (RectangleSnip, WindowSnip, FreeformSnip, RectangleRecord).

> [!IMPORTANT]
> If no **enabledModes** parameter is specified, the default behavior will allow all modes.

## Examples

### Example 1: Enable Only Rectangle Snip

`ms-screenclip://capture/image?rectangle&enabledModes=RectangleSnip&redirect-uri=my-snip-protocol-test-app://response`

*Explanation: This command launches the Snipping Tool with only the rectangle snipping option enabled. The user will only be able to select a rectangular region for capture.*

### Example 2: Enable Rectangle Snip and Window Snip

`ms-screenclip://capture/image?rectangle&enabledModes=RectangleSnip,WindowSnip&redirect-uri=my-snip-protocol-test-app://response`

*Explanation: This command launches the Snipping Tool with both the rectangle and window snipping modes enabled. The user can choose between capturing a rectangular area or an entire window.*

### Example 3: Enable All Snipping Modes

`ms-screenclip://capture/image?rectangle&enabledModes=SnippingAllModes&redirect-uri=my-snip-protocol-test-app://response`

*Explanation: This command launches the Snipping Tool with all supported image snipping modes (RectangleSnip, WindowSnip, FreeformSnip). The FullScreenSnip mode is excluded from interactive mode and will not be enabled.*

### Example 4: Enable Recording Mode Only

`ms-screenclip://capture/video?enabledModes=RecordAllModes&redirect-uri=my-snip-protocol-test-app://response`

*Explanation: This command launches the Snipping Tool with only the recording mode enabled. The user can only choose the rectangle recording mode.*

### Example 5: Enable Multiple Snipping and Recording Modes

`ms-screenclip://capture/image?enabledModes=RectangleSnip,RectangleRecord&redirect-uri=my-snip-protocol-test-app://response`

*Explanation: This command launches the Snipping Tool with both rectangle snip and rectangle recording modes available. Users can either snip a rectangle or record the selected area.*

## Key considerations

- **Mode Restrictions:** Developers should ensure that enabling specific modes aligns with the expected behavior of their application. Restricting UI options helps maintain a consistent user experience and ensures the resulting capture matches the application's needs.
- **Unsupported Modes:** The FullScreenSnip mode is not supported in interactive mode and should not be used in the enabledModes parameter.
- **Default Behavior:** If no enabledModes parameter is specified, all modes (RectangleSnip, WindowSnip, FreeformSnip, RectangleRecord) are available by default.

## Query

**ms-screenclip:**

| Parameter                | Type            | Required | Description                                                                 | Default           |
|--------------------------|-----------------|----------|-----------------------------------------------------------------------------|-------------------|
| api-version              | string          | "1.0"    | Protocol version (e.g., "1.0"). This ensures compatibility and supports future enhancements. | "preview"         |
| user-agent               | string          | yes      | Identifier for the calling application, used for logging and analytics.     | n/a               |
| x-request-correlation-id | string          | no       | A unique identifier value attached to requests and messages that allow reference to a particular transaction or event chain. | Generated Guid if not provided. |
| rectangle                | (image & video) | no       | Specifies the capture area as x,y,width,height. Leave Blank for interactive mode. | Interactive Mode  |
| Window                   | (Image)         | no       | Target window specified by hwnd. Leave Blank for interactive mode.          | Interactive Mode  |
| Freeform                 | (Image)         | no       | Lets the user capture a freeform snip.                                      | Interactive Mode  |
| FullScreen               | (Image)         | no       | Captures the full screen snip.                                              | Auto Mode         |
| redirect-uri             | URI             | yes      | Callback URI protocol for the response. Applications must register a handler for this protocol. | n/a               |

## Parameter validation

The following validation checks should be performed on the parameters:

- **Parameter Sanitization:** Validate and sanitize all input parameters to prevent injection attacks.
- **Protocol Validation:** Ensure that the callback protocol string is validated against a list of allowed protocols to prevent injections or execution of malicious code.
- **Required Fields:** Check that all required fields are provided and valid before proceeding with the snip operation.

Response if expected parameters **aren't** supplied or overloaded.

## Responses to the caller

To ensure the response back to the caller via `redirect-uri` follows HTTP-based interaction principles, the response will mimic the structure of an HTTP response but will be conveyed through URI query parameters. This approach keeps the interaction web-standard compliant and familiar to developers.

### Use of shared tokens

The use of the `SharedStorageAccessManager` class and of sharing tokens is subject to the following requirements and restrictions:

- A sharing token can only be redeemed one time. After that, the token is no longer valid.
- A sharing token expires after 14 days and is no longer valid.
- The source app cannot provide more than one thousand sharing tokens. After a token is redeemed, removed, or expires, however, it no longer counts against the quota of the source app.

### Response parameters

The following parameters are returned in the redirect URI:

| Parameter               | Type   | Description                                                                                                      |
|-------------------------|--------|------------------------------------------------------------------------------------------------------------------|
| Reason                  | String | The outcome and explanation for the shipping outcomes.                                                           |
| Token (for success)     | String | A token representing the captured media, which the application can use to access the file.                       |
| code                    | Int    | The HTTP status code equivalent to provide a more granular understanding of the outcome.                         |
| x-request-correlation-id| String | A unique identifier value attached to requests and messages that allow reference to a particular transaction or event chain. |

## Retrieving a token

A sample application is available to test the process of calling the protocol and converting the response token into media. Use the [SharedStorageAccessManager](/uwp/api/windows.applicationmodel.datatransfer.sharedstorageaccessmanager) library to obtain the token.

The sample app code for retrieving tokens is available [here](https://microsoft.visualstudio.com/Apps/_git/SnipProtocolTestApp?path=/SnipProtocolTestApp/MainPage.xaml.cs&version=GBmaster&line=139&lineEnd=140&lineStartColumn=1&lineEndColumn=1&lineStyle=plain&_a=contents).

## Status codes

The following table lists the status codes that can be returned in the redirect URI:

| HTTP Status Code | Reason                                         | Description                                                                 |
|------------------|------------------------------------------------|-----------------------------------------------------------------------------|
| 200              | Success                                        | The operation was successful.                                               |
| 400              | Bad Request - Invalid or Missing Parameters    | The request cannot be processed due to client error.                        |
| 408              | Request Timeout - Operation Took Too Long      | The operation timed out before completion.                                  |
| 499              | Client Closed Request - User Cancelled the Snip| The user cancelled the snip, closing the request.                           |
| 500              | Internal Server Error - Processing Failed      | An error occurred on the server, preventing completion.                     |

## Example responses

| Use Case           | Full URI Example                                                                                                                                |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| Successful Capture | `my-snip-protocol-test-app://response/?code=200&reason=Success&request-correlation-id=CF99C5A5-3907-461E-A9A9-D8AAFFAD5031&token=8930-ASDFA-ASDF4545` |
| Failed Capture     | `my-snip-protocol-test-app://response/?code=400&reason=Bad%20Request%20-%20Invalid%20value%20Missing%20Parameters&request-correlation-id=C7696B38-52C8-419A-880F-F3350D7A6626`  |

## Caller example

Below is a table displaying examples of full URIs constructed to initiate different types of snipping sessions using the screenclip: protocol. Each URI example demonstrates a combination of parameters to illustrate how you can customize the snipping tool's behavior for different use cases.

| Use Case                     | Example URI                                                                                                                                            | Description                                                                                                      |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| Rectangle Mode - Interactive | `ms-screenclip://capture/image?user-agent=TestApp&Rectangle&uri=my-snip-protocol-test-app://response`                                                     | An application initiates an interactive rectangle capture session, where the user selects the capture area. The result is redirected to a specific URI. |
| Video Mode - Interactive     | `ms-screenclip://capture/video?api-version=1.0&user-agent=TestApp&redirect-uri=my-snip-protocol-test-app://response`                                      | A video capture. Always in rectangle mode. |

## Related content

- [Use Snipping Tool to capture screenshots](https://support.microsoft.com/windows/use-snipping-tool-to-capture-screenshots-00246869-1843-655f-f220-97299b865f6b)
- [Launch screen snipping (Legacy)](launch-screen-snipping.md)
