# Bridge Daemon

// BridgeService defines the gRPC service used by bridge daemon.

// Sends a list of newly recognized bridge events.

rpc AddBridgeEvents(AddBridgeEventsRequest)

returns (AddBridgeEventsResponse);

// AddBridgeEventsRequest is a request message that contains a list of new bridge

// events. The events should be contiguous and sorted by (unique) id.

message AddBridgeEventsRequest {

repeated dydxprotocol.bridge.BridgeEvent bridge\_events = 1

\[ (gogoproto.nullable) = false ];

// AddBridgeEventsResponse is a response message for BridgeEventRequest.

message AddBridgeEventsResponse {}
