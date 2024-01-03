# x/bridge module

rpc EventParams(QueryEventParamsRequest)

returns (QueryEventParamsResponse);

rpc SafetyParams(QuerySafetyParamsRequest)

returns (QuerySafetyParamsResponse);

rpc ProposeParams(QueryProposeParamsRequest)

returns (QueryProposeParamsResponse);

rpc NextAcknowledgedEventId(QueryNextAcknowledgedEventIdRequest)

returns (QueryNextAcknowledgedEventIdResponse);

rpc NextRecognizedEventId(QueryNextRecognizedEventIdRequest)

returns (QueryNextRecognizedEventIdResponse);

message QueryEventParamsRequest {}

message QueryEventParamsResponse {

message QuerySafetyParamsRequest {}

message QuerySafetyParamsResponse {

message QueryProposeParamsRequest {}

message QueryProposeParamsResponse {

ProposeParams params = 1;

message QueryNextAcknowledgedEventIdRequest {}

message QueryNextAcknowledgedEventIdResponse {

message QueryNextRecognizedEventIdRequest {}

message QueryNextRecognizedEventIdResponse {
