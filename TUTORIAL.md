# 1 Create project folder FLASK-API-SQLALCHEMY

# 2 Install virtual env 
> pip install virtualenv

# 3 Create virtualenv , provide a name for that folder ( venv in this case)
> virtualenv venv

# 4 Activate virtual env
> ./venv/Scripts/activate 

# 5 Install flask
> pip install flask flask-sqlalchemy

# 6 Install marshmellow to define squema
> pip install flask-marshmellow marshmellow-sqlalchemy

# 7 Install pymysql module to connect with mysql
>pip install pymysql

# 8 Create src folder and app.py file

# 9 Import flask, sqlalchemy

# 10 Create an instance of Flask 
app = Flask(__name__)

# 11 Config an MySql connection
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+pymysql://root@localhost/flaskmysql'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

# 12 Create an Instance fir the database ( an object)
db = SQLAlchemy(app)

# 13 Create an Instance  for marshemellow to complete a basic app
ma = Marshmellow(app)

# 14 Define the data model for the database, create a task class anda add some properties, this properties are equivalente to table columns.
class Task(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(70), unique=True)
    description = db.Column(db.String(100))

# 15 Define a function called init (constructor) that will be executed in every instance of this class
def __init__(self, title, description):
        self.title = title
        self.description = description

# 16 Use the method db.create_all() This method creates a table for every class.
db.create_all()

# 17 Create a class schema and import marshmellow (ma), then define the fields to obtain from the schema.
class TaskSchema(ma.Schema):
    class Meta:
        fields = ('id', 'title', 'description')

# 18 Create an instance of TaskSchema to retrieve any task, and another instance to retrieve all tasks
task_schema = TaskSchema()
tasks_schema = TaskSchema(many=True)

# 19 Define Routes (End Points)
