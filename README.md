const express = require('express')
const { v4: uuidv4 } = require('uuid');
const app = express()
app.use(express.json())

const alunos = {}

app.get('/', (req, res) => {
    res.json({msg: "Hello From Express!!"})
})

app.post('/alunos', (req, res) => {
    const aluno = req.body
    const idAluno = uuidv4()
    console.log(aluno)
    aluno.id = idAluno
   
    alunos[idAluno] = aluno
    res.json({msg: "Aluno adicionado com sucesso!!"})
})


app.get('/alunos', (req, res) => {
    res.json({alunos: Object.values(alunos)})
})

app.put('/alunos', (req, res) => {
    const id = req.query.id
    if (id && alunos[id]){
        const aluno = req.body
        aluno.id = id
        alunos[id] = aluno
        res.json({msg: "Aluno atualizado com sucesso!!"})
    }else{
        res.status(400).json({msg: "Aluno não encontrado!!"})
    }

})

app.delete('/alunos', (req, res) => {
    const id = req.query.id
    if (id && alunos[id]){
        delete alunos[id]
        res.json({msg: "Aluno deletado com sucesso!!"})
    }else{
        res.status(400).json({msg: "Aluno não encontrado!!"})
    }
})

app.listen(8080, () => {
    console.log('Bem-vindo ao meu servidor!! ')
})
