These are the changes I've made to Udacity's Intro to Backend hw4 so that it uses ndb instead of db.

Please feel free to make a pull request if you notice any errors.

1) line 11 Change from google.appengine.ext import db to

from google.appengine.ext import ndb

2) line 89 class change User(db.Model) to 

class User(ndb.Model):
    name = ndb.StringProperty(required = True)
    pw_hash = ndb.StringProperty(required = True)
    email = ndb.StringProperty()


3) line 100
Change u = User.all().filter('name =', name).get()

u = User.query().filter(ndb.GenericProperty('name')==name).get()

4) line 87

Change return db.Key.from_path('users', group) to:

return ndb.Key('users', group)

5) line 53

Change self.set_secure_cookie('user_id', str(user.key().id())) to

self.set_secure_cookie('user_id', str(user.key.id()))

This is in addition to the Post changes listed in the hw3 README.md at 

https://github.com/reneesmacdonald/hw3ndb/blob/master/README.md
