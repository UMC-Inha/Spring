## ERD Preview

![ERD 사진](./erd.png)

## 미션 2-1

![미션 2-1](./2-1.png)

```sql
-- OFFSET 기반 --
SELECT
    s.name AS store_name,
    m.contents,
    m.point,
    um.startdate
FROM
    mission m
    JOIN store s ON m.store_id = s.id
    JOIN usermission um ON m.id = um.missionid
WHERE
    um.userid = <userid> AND
    (um.status = 'PENDING' OR um.status = 'SUCCESS')
ORDER BY um.startdate DESC, m.id, um.userid;
LIMIT <limit_value> OFFSET <offset_value>;
-- CURSOR 기반 --
SELECT
    s.name AS store_name,
    m.contents,
    m.point,
    um.startdate
FROM
    mission m
    JOIN store s ON m.store_id = s.id
    JOIN usermission um ON m.id = um.missionid
WHERE
    um.userid = <userid> AND
    um.missionid = <missionid> AND
    (um.status = 'PENDING' OR um.status = 'SUCCESS') AND
    (
        (um.startdate, m.id, um.userid) > ('<last_startdate>', <last_mission_id>, <last_userid>) OR
        (um.startdate = '<last_startdate>' AND m.id > <last_mission_id>) OR
        (um.startdate = '<last_startdate>' AND m.id = <last_mission_id> AND um.userid > <last_userid>)
    )
ORDER BY um.startdate DESC, m.id, um.userid
LIMIT <limit_value>;
```

## 미션 2-2

![미션 2-2](./2-2.png)

```sql
INSERT INTO Review (reviewid, storeid, score, content)
VALUES ('<reviewid>', '<storeid>', <score>, '<content>');
```

## 미션 2-3

![미션 2-3](./2-3.png)

```sql
-- Cursor 기반 --
SELECT
	s.name AS store_name,
	s.type,
	m.contents,
	m.point,
	m.duedate
FROM
	mission m
	JOIN store s ON m.store_id = s.id
	LEFT JOIN usermission um ON m.id = um.missionid AND um.userid = <userid>
WHERE
	um.missionid IS NULL AND
	s.regionid = <regionid> AND
	m.duedate > NOW() AND
	(
		(m.duedate, m.id) > ('<last_duedate>', <last_mission_id>) OR
		(m.duedate = '<last_duedate>' AND m.id > <last_mission_id>)
	)
ORDER BY m.duedate, m.id
LIMIT <limit_value>;
-- OFFSET 기반 --
SELECT
    s.name AS store_name,
    s.type,
    m.contents,
    m.point,
    m.duedate,
FROM
    mission m
    JOIN store s ON m.store_id = s.id
    LEFT JOIN usermission um ON m.id = um.missionid
WHERE
    um.userid = NULL AND
    s.regionid = <regionid>
    m.duedate > NOW() AND
ORDER BY um.startdate, m.id, um.userid;
LIMIT <limit_value> OFFSET <offset_value>;
```

## 미션 2-4

![미션 2-4](./2-4.png)

```sql
-- 최신 포인트를 가져오기 위해 LIMIT 1 사용 --
-- 전화번호 인증이 없으면 null 반환 --
SELECT
	u.name,
	u.nickname,
	u.email,
	u.phonenum,
	p.point,
FROM
	user u
	JOIN point p ON u.id = p.userid
WHERE
	u.id = <userid>
ORDER BY p.id
LIMIT 1;
```
