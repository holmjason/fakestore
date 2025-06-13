import axios from "axios";
import { useState, useEffect} from "react";
import Container from 'react-bootstrap/Container';
import Form from 'react-bootstrap/Form';
import Button from 'react-bootstrap/Button';
import Alert from 'react-bootstrap/Alert';
import ProductDetails from "./ProductDetails";
import { useParams } from "react-router-dom";

function EditProduct() {
    const [submitted, setSubmitted] = useState(false);
    const [error, setError] = useState(null);
    const [formData, setFormData] = useState({
        title: '',
        description: '',
        category: '',
        price: '',
        image: '',
    });
    const { id } = useParams();

    const handleChange = (e) => {
        const { name, value } = e.target;
        setFormData(prev => ({
            ...prev,
            [name]: value
        }));
    };

    const handleSubmit = async (event) => {
        event.preventDefault();
        try {
            await axios.put(`https://fakestoreapi.com/products/${id}`, formData);
            setSubmitted(true);
            setError(null);
        } catch (err) {
            setError('Failed to update product');
        }
    };
     useEffect(() => {
        if (id) {
            axios.get(`https://fakestoreapi.com/products/${id}`)
                .then(res => setFormData({
                    title: res.data.title,
                    price: res.data.price,
                    description: res.data.description,
                    category: res.data.category,
                    image: res.data.image
                }))
                .catch(error => setError('Failed to fetch product'));
        }
    }, [id]);

    return (
        <Container>
            <h2>Edit Product</h2>
            {submitted && <Alert variant="success">Product updated!</Alert>}
            {error && <Alert variant="danger">{error}</Alert>}
            <Form onSubmit={handleSubmit}>
                <Form.Group>
                    <Form.Label>Title</Form.Label>
                    <Form.Control
                        type="text"
                        name="title"
                        value={formData.title}
                        onChange={handleChange}
                    />
                </Form.Group>
                <Form.Group>
                 <Form.Label>Price</Form.Label>
                    <Form.Control
                        type="number"
                        name="price"
                        value={formData.price}
                        onChange={handleChange}
                    />
                </Form.Group>
                {/* Add other fields as needed */}
                <Button type="submit">Update</Button>
                <button type="delete" onClick={() => axios.delete(`https://fakestoreapi.com/products/${id}`)}>Delete</button>
            </Form>
        </Container>
        
        
    );
}

export default EditProduct;
