# Disclaimer
This is a fork of the original [convert-firebase-timestamp](https://github.com/peterkracik/convert-firebase-timestamp) library written by [https://github.com/peterkracik](@peterkracik).  
Everything has been created by the original contributor(s) except commit [4a395490](https://github.com/mihaly044/convert-firebase-timestamp/commit/4a39549066068cd182241e2a3738fdacae3e48ce) that fixes a minor bug.

# Convert firebase timestamps

Script that converts firebase timestamp values to the JS date format

* converts each timestamp within a document (object), also inside its maps and array
* converts single value
* possible to call in rxjs pipe

## How to use

**document**

```typescript
 return this.db.collection('my-collection').doc(id).snapshotChanges().pipe(
    map(doc => convertTimestamps(doc.payload.data())
)
```

**single value**

```typescript
return this.db.collection('my-collection').doc(id).snapshotChanges().pipe(
    map(doc => {
		const data = doc.payload.data();
		data.date = convertTimestamp(data.date);
		return data;
	})
)
```
**in pipe**
! don't call it before map, the original document is too large to be convert and it will throw recursion exception

```typescript
return this.db.collection('my-collection').doc(id)
  .snapshotChanges().pipe(
        map(doc => doc.payload.data()),
        convertTimestampsPipe(),
    );
)
```
