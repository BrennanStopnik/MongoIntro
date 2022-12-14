## Mongo Assignment 1 - Part 1:

- Create a new github repo:
	- The title will be MongoIntro
	- _Important_: Initalize the repo WITH a README
	- Clone the repo to your computer and add the link to populi
- For the assignment, you will write out your queries in NoSQLBooster and then copy/paste the final queries into the README and commit
- Create a new database BlogsDB and a new collection blogs
- Insert the 10 sample blogs into the blogs collection with the following data types per field:
	- _Note_: You will need to modify some of the blog fields to be the proper data types before inserting into the collection. E.G. objectId needs to be a number instead of a string.
	- "createdAt": {Date},
	- "title": {String},
	- "text": {String},
	- "author": {String},
	- "lastModified": {Date},
	- "categories": {String[]},
	- "id": {String},
	- "objectId": {Number}
- Write the following queries and add them to the README:
	- Insert a new blog into the collection
		- _Note_: Field data types must match sample blog data types
	- Find one blog by author
	- Find all blogs whose objectId is greater than 5
	- Find all blogs whose createdAt is after April 1, 2022


## Mongo Assignment 1 - Part 2:

- Write the following queries and add them to the README:
	- Find all blogs where the field lastModified does not exist and 
	- Find all blogs where the createdAt type is a date
	- Combine the above two queries into one to find all blogs in which lastModified does not exist and createdAt is the type date
- _Stretch_ 
	- Find a blog with a specific phrase (or a more complex regular expression if you want to practice regexs) in the text
	- Find all blogs that have "qui" in the categories array

## Mongo Assignment 1 - Part 3:

- Write the following queries and add them to the README:
	- Find all blogs in which the lastModified does not exist and set it
	- From now on, all the following queries should update lastModified to be the current datetime 
	- Find all blogs created after May 2022 and add "lorem" as a new category in the categories array
	- Find all blogs that have the category "voluptas" and pull "voluptas" from the categories
	- Find all blogs with "corrupti" in the categories and delete those blogs


## Assignment Results

### Part 1

#### - Add all blogs
const newBlogPosts = [blog1, blog2, blog3,  blog4, blog5, blog6, blog7, blog8, blog9, blog10]
db.posts.insertMany(newBlogPosts)

#### - Add single blog
db.posts.insertOne(blog11)

#### - Find single blog by author
db.posts.find({
    author: {
        $regex: /Turd/
    }
})
   .projection({})
   .sort({_id:-1})
   .limit(100)

#### - Greater than 5
db.posts.find({
    objectId: {
        $gt: 5
    }
})
   .projection({})
   .sort({_id:-1})
   .limit(100)

#### - CreatedAt greater than 4/1/2022
db.posts.find({
    createdAt: {
        $gt: new Date("4/1/2022")
    }
})
   .projection({})
   .sort({_id:-1})
   .limit(100)

### Part 2

#### - LastModified does not exist
db.posts.find({
    lastModified: {
        $exists: false
    }
})
   .projection({})
   .sort({_id:-1})
   .limit(100)

#### - CreatedAt type is a date
db.posts.find({
    createdAt: {
        $type: "date"
    }
})
   .projection({})
   .sort({_id:-1})
   .limit(100)

#### - LastModified and CreatedAt in one
db.posts.find({
    lastModified: {
        $exists: false
    },
    createdAt: {
        $type: "date"
    }
})
   .projection({})
   .sort({_id:-1})
   .limit(100)

#### - Regex for a phrase
db.posts.find({
    text: {
        $regex: /veritatis aliquam/
    }
})
   .projection({})
   .sort({_id:-1})
   .limit(100)

#### - Blogs with qui in categories
db.posts.find({
    categories: {
        $in: ["qui"]
    }
})
   .projection({})
   .sort({_id:-1})
   .limit(100)


### Part 3

#### Set LastModified
db.posts.updateMany({
    lastModified: {
        $exists: false
    }
},{
    $set:{
        lastModified: new Date()
    }
})

### Add lorem and update lastModified
db.posts.updateMany({
    createdAt: {
        $gt: new Date("5/1/2022")
    }
},{
    $addToSet: {
        categories: "lorem"
    },
    $set: {
        lastModified: new Date()
        
    }
})

### Find "voluptas" and pull from catorgies
db.posts.updateMany({
    categories: {
        $in: ["voluptas"]
    }
},{
    $pull: {
        categories: "voluptas"
    },
    $set: {
        lastModified: new Date()
    }
})

### Delete blogs with corrupti in categories
db.posts.deleteMany({
    categories:{
        $in: ["corrupti"]
    }
})




## - All blogs data as variables with the new one added to the end as number 11

const blog1 = {
    createdAt: new Date("2022-04-16T06:33:29.080Z"),
    title: "fugiat",
    text: "Voluptates dicta ut dolorem dolor. Tempora animi facilis dignissimos nostrum tempora soluta asperiores. Aut velit aspernatur rerum doloribus. Voluptate non voluptate consequatur. Et qui recusandae aliquid autem consequatur necessitatibus dolore aut.\nSimilique tempora iure magni. Ut eos eveniet amet officiis ab dicta explicabo est eos. Aperiam sunt ullam ipsam iste. Quam dolorum omnis minus sapiente. Est perferendis aut at non aut est ducimus asperiores porro. Rerum et vero perspiciatis ea facere omnis dolor dolores qui.\nNon voluptates aliquam et praesentium vero adipisci odio. Atque et molestias. Accusamus optio suscipit consequatur necessitatibus possimus ut nostrum et pariatur. Aut nam repellendus ut voluptate molestias et sint. Excepturi et ullam dolor ipsa nulla sapiente et. Suscipit quo consequatur voluptatem qui neque voluptatem voluptate ex.",
    author: "Ronald Barrows",
    lastModified: new Date(),
    categories: ["nulla", "quasi", "beatae"],
    id: "dcc2102d-a20a-4765-8dc4-9079af4fdc9b",
    objectId: 1
}

const blog2 = {
    createdAt: new Date("2022-08-23T11:58:31.513Z"),
    title: "esse",
    text: "Soluta reprehenderit autem exercitationem. Laborum eum ratione. Quo ipsum necessitatibus eius similique architecto magnam adipisci dolorem. Inventore odio quia vel cupiditate non. Occaecati ex quia porro numquam voluptatibus sed ut occaecati.\nDolor quae velit a possimus earum. Ut itaque deserunt aut ab. Sed quam laborum fuga rerum sit dolorem qui in. Error laboriosam qui. Recusandae nam minus et cupiditate quasi tempore.\nSit quidem labore voluptatem nisi laudantium. Officiis quos architecto voluptatum ut. Molestias ut modi officiis sequi tenetur et expedita voluptatem molestiae. Possimus modi unde possimus non facere maiores inventore libero dolore.",
    author: "Ellen Schmidt III",
    lastModified: new Date(),
    categories: ["quia", "corrupti", "eaque"],
    id: "d9e1d991-2e30-4a1f-8d07-6040a8e5fd68",
    objectId: 2
}

const blog3 = {
    createdAt: new Date("2022-01-24T02:29:08.292Z"),
    title: "temporibus",
    text: "Ipsa provident at ipsa recusandae nam explicabo. Itaque iure eum ratione aut quaerat. Error reiciendis sed quisquam mollitia quisquam occaecati consequatur. Odit laboriosam aut voluptatem sunt voluptas possimus quaerat. Sed est aut eius. Et nihil omnis unde autem distinctio dolorem non.\nRepellat consequatur non est ipsa voluptatibus atque. Aperiam qui ipsum. Officiis aut voluptatum beatae accusantium et. A eaque architecto tempora fugit amet quaerat expedita in. Est quaerat ea quia itaque nulla consequuntur et. Ut vel est odio.\nCupiditate animi delectus aut. Pariatur deleniti pariatur sed incidunt iure qui minus. Ut sapiente quibusdam autem sapiente aut sit et voluptatem. Vero voluptatem iste quia. Beatae sint veniam voluptatem.",
    author: "Miss Sherry Rohan",
    lastModified: new Date(),
    categories: ["tempore", "totam", "voluptas"],
    id: "7e2361f5-7648-4532-94fa-366ed86cf147",
    objectId: 3
}

const blog4 = {
    createdAt: new Date("2022-07-28T02:46:19.103Z"),
    title: "optio",
    text: "Quia rerum pariatur ipsa doloremque aperiam ad commodi. Numquam sit recusandae ea qui harum autem voluptatem asperiores. Nisi repudiandae qui vero distinctio vel a.\nSint ut non quae. Consectetur rerum veritatis aliquam enim consectetur corrupti. Distinctio assumenda excepturi tempora quo quidem consequatur. Labore qui nihil qui dolores quae ipsum est quod. Est impedit qui hic nobis et natus et. Et corrupti quia rerum.\nCumque qui doloremque fuga. Non sed reiciendis voluptate unde qui blanditiis et. Molestiae consequatur corporis est cum odit voluptatibus. Ea ad vitae dignissimos. Et nam ut numquam iste est explicabo perferendis. Sunt atque quo maxime asperiores ut.",
    author: "Paula Boyer",
    lastModified: new Date(),
    categories: ["voluptas", "corrupti", "debitis"],
    id: "d8d67722-ad63-4700-9654-cebdf19009e0",
    objectId: 4
}

const blog5 = {
    createdAt: new Date("2021-10-02T08:46:06.390Z"),
    title: "id",
    text: "Earum iste cumque voluptatem velit facilis et quasi et itaque. Voluptatibus voluptatibus quam. Sit sequi nulla eum. Animi doloremque eos molestiae dolorum atque aut. Est itaque odio accusamus minima tempora enim animi. Sint quam vitae pariatur tempore velit pariatur aliquid.\nOmnis molestiae maxime. Ratione et ducimus itaque. Omnis ut et delectus est officiis quaerat mollitia debitis saepe. Tempore non quod nesciunt rem necessitatibus cupiditate. Sed reprehenderit eius possimus. Inventore accusamus incidunt excepturi aut eum ipsam cupiditate asperiores.\nAperiam atque explicabo velit. Labore cumque debitis tenetur. Quo autem aut provident. Nihil nihil natus libero sit. Sunt at et.",
    author: "Brett Wolf",
    lastModified: new Date(),
    categories: ["hic", "qui", "sequi"],
    id: "01ac5582-4c44-45f3-b3c1-f35db0edc29e",
    objectId: 5
}

const blog6 = {
    createdAt: new Date("2022-01-27T07:59:32.530Z"),
    title: "ipsum",
    text: "Voluptate sequi perferendis id repellendus voluptate et quaerat et qui. Sunt qui necessitatibus aut aut perferendis. Suscipit mollitia laudantium atque doloribus repellat.\nEst culpa iste eius impedit incidunt rem maiores. Dolorem sit quod nihil. Ipsam dolore et doloribus odio. Quibusdam ea deleniti quo qui. Et doloremque omnis pariatur explicabo aliquid impedit.\nSaepe ex error nostrum facere corrupti ut. Voluptatem quo aut suscipit autem. Dicta a sint. Beatae excepturi rem adipisci quaerat quia dolorem labore. Exercitationem totam explicabo harum modi voluptas molestiae facilis.",
    author: "Penny Weissnat",
    lastModified: new Date(),
    categories: ["saepe", "ut", "dolorem"],
    id: "a2c15b3c-f687-4ee8-9a04-24fb30b8f1e1",
    objectId: 6
}

const blog7 = {
    createdAt: new Date("2022-02-02T20:23:59.817Z"),
    title: "animi",
    text: "Sed officiis autem quaerat ipsa expedita eum nihil enim architecto. Ut aut quibusdam. Sunt maiores occaecati velit odio praesentium consequatur qui vero rerum. Delectus sint dolore.\nAccusamus et officia aliquid debitis deserunt. Non quaerat vel. Enim modi ducimus adipisci eos ut occaecati incidunt optio. Ea omnis nisi iure nemo unde laborum maiores. Sed inventore aliquid sit ad.\nUt quidem dolor molestiae sit aut a exercitationem. Vel similique sunt molestiae dolorum rem eaque soluta repellat. Magni est iure omnis laborum.",
    author: "Ramona Bartell",
    lastModified: new Date(),
    categories: ["veritatis", "dolorem", "deserunt"],
    id: "976604e5-b10f-47fb-9191-dcb23df24277",
    objectId: 7
}

const blog8 = {
    createdAt: new Date("2021-10-19T19:12:00.530Z"),
    title: "accusamus",
    text: "Cum architecto molestiae voluptatem commodi excepturi. Vero unde voluptatibus perferendis repellendus in voluptatum voluptates doloremque. Velit perspiciatis assumenda est temporibus. Ipsa natus a est voluptate. Repellat nihil inventore optio optio quaerat laborum itaque error.\nExplicabo rerum omnis nemo dolorem impedit. Qui explicabo maiores. Aut hic rerum atque eos dolores.\nEos quia optio quae esse. Sit reiciendis repellat at soluta sunt incidunt minima magnam quod. Magni enim est quia nam. Fugiat vitae et asperiores laboriosam. Ut neque qui. Quia dolor ex aut adipisci.",
    author: "Brandi Feil",
    lastModified: new Date(),
    categories: ["quia", "ea", "et"],
    id: "e39a30b5-4507-4d6f-b9cf-72e4c7d3c779",
    objectId: 8
}

const blog9 = {
    createdAt: new Date("2022-09-09T12:56:17.262Z"),
    title: "delectus",
    text: "Et natus maiores. Aut voluptatem autem velit aspernatur recusandae delectus cupiditate iste quia. Qui velit voluptas. Tempora facere repudiandae molestias sunt officia ut magnam dolor voluptatem. Voluptas iste aliquid consectetur. Numquam voluptas facilis vitae.\nDeserunt quia sunt. Natus delectus rerum ducimus aut qui amet vel molestias. Est natus nesciunt nemo temporibus labore. Maxime recusandae perferendis velit voluptatum vitae.\nRerum voluptatem in. Occaecati ea odit eius beatae facere ea quasi et. Nostrum illo doloremque reprehenderit excepturi omnis.",
    author: "Kelly Barton",
    categories: ["esse", "dolor", "qui"],
    id: "01ed79b1-75c2-44e5-becb-10788158a7db",
    objectId: 9
}

const blog10 = {
    createdAt: new Date("2022-01-14T15:07:41.214Z"),
    title: "aliquam",
    text: "Nulla expedita libero ut accusantium vitae repellat et. Accusantium ipsa expedita ratione harum provident quia totam. Dicta facilis dicta saepe et. Est et delectus veritatis nihil. Magnam dolor iste perspiciatis officia blanditiis possimus.\nTotam alias corrupti doloribus. Nihil laboriosam expedita omnis nihil. Eos delectus nulla sit magni aut quae distinctio deserunt.\nAutem et aliquam quasi nam. Vero enim ullam voluptas ut quidem libero rerum. Nam omnis illo voluptatem non tempore ipsum. Qui nulla fugiat rerum.",
    author: "Alfred Davis",
    categories: ["rerum", "mollitia", "voluptas"],
    id: "4a571289-6d5c-4300-9614-53c6e1237d81",
    objectId: 10
}
    
const blog11 = {
 createdAt: new Date("2022-01-14T15:07:51.214Z"),
 title: "hamjam",
 text: "Nulla expedita libero ut accusantium vitae repellat et. Accusantium ipsa expedita ratione harum provident quia totam. Dicta facilis dicta saepe et. Est et delectus veritatis nihil. Magnam dolor iste perspiciatis officia blanditiis possimus.\nTotam alias corrupti doloribus. Nihil laboriosam expedita omnis nihil. Eos delectus nulla sit magni aut quae distinctio deserunt.\nAutem et aliquam quasi nam. Vero enim ullam voluptas ut quidem libero rerum. Nam omnis illo voluptatem non tempore ipsum. Qui nulla fugiat rerum.",
 author: "Turd Fergusson",
 lastModified: new Date(),
 categories: ["rektum", "lollitia", "voluptuous"],
 id: "4a571289-6d5c-4300-9614-53c6e1294b71",
 objectId: 11
}
 
